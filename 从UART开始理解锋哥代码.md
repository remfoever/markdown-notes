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







