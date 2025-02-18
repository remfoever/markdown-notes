# 初始化配置

```c
/* This is the configuration of the UART-driver */
WxUartDriverCfg g_WxUartDriverCfg = {
    .uartDevId = XPAR_XUARTPS_0_DEVICE_ID,
    .taskPri = 5,
    .baudRate = 115200,
    .dataBits = 8,
    .stopBits = 1,
    .parity = 0,
    .operMode = XUARTPS_OPER_MODE_NORMAL,
    .intrId = XPAR_XUARTPS_0_INTR,
};
```

首先配置的全局变量  **g_WxUartDriverCfg**

```c
/* Initialize the UART driver */

UINT32 WX_UART_DRIVER_Configure(WxUartDriver *this, WxUartDriverCfg *cfg)
{
    /* Find and initialize the UART configuration */
    XUartPs_Config *config = XUartPs_LookupConfig(cfg->uartDevId);
    if (config == NULL) {
        return WX_UART_DRIVER_CFG_FIND_FAIL;
    }
    /* Initialize the UART instance */
    XStatus status =
        XUartPs_CfgInitialize(&this->uartInst, config, config->BaseAddress);
    if (status != WX_SUCCESS) {
        return WX_UART_DRIVER_CFG_INIT_FAIL;
    }
    /* Create a structure to configure the UART format */
    XUartPsFormat uartFormat = {.DataBits = cfg->dataBits,
                                .StopBits = cfg->stopBits,
                                .Parity = cfg->parity};
    /* Configure the UART */
    XUartPs_SetOperMode(&this->uartInst, cfg->operMode);
    XUartPs_SetBaudRate(&this->uartInst, cfg->baudRate);
    /* Configure the data format */
    XUartPs_SetDataFormat(&this->uartInst, &uartFormat);

    return WX_SUCCESS;
}

```

初始化串口驱动的所有配置即所有	**g_WxUartDriverCfg** 	参数  到	**this**	*（WxUartDriver）* 中，因为所有接口统一到  **WxUartDriver**



设置中断系统

```c
UINT32 WX_UART_DRIVER_SetupInterruptSystem(
    WxUartDriver *this, WxUartDriverCfg *cfg,
    VOID (*handLer)(VOID *callBackRef, UINT32 event, UINT32 eventData))
{
    /* Initialize the interrupt controller */
    XUartPs *uartInstPtr = &this->uartInst;
    XScuGic *intcPtr = WX_GetScuGicInstance();
    if (intcPtr == NULL) {
        return WX_UART_DRIVER_INTC_INIT_FAIL;
    }
    /* Connect the interrupt signal to the handler function */
    int status = XScuGic_Connect(intcPtr, cfg->intrId,
                                 (Xil_ExceptionHandler)XUartPs_InterruptHandler,
                                 uartInstPtr);
    if (status != WX_SUCCESS) {
        return WX_UART_DRIVER_INTC_CONNECT_FAIL;
    }
    /*
     * Set the handler function for the interrupt signal. The handler function
     * will be called when the interrupt signal is asserted.
     */
    XUartPs_SetHandler(uartInstPtr, (XUartPs_Handler)handLer, this);
    /* Enable the interrupt signal */
    XUartPs_SetInterruptMask(uartInstPtr, XUARTPS_IXR_RXOVR | XUARTPS_IXR_TOUT |
                                              XUARTPS_IXR_OVER);
    XUartPs_SetRecvTimeout(uartInstPtr, 8);
    /* Enable the interrupt in the interrupt controller */
    XScuGic_Enable(intcPtr, cfg->intrId);
    return WX_SUCCESS;
}
```





