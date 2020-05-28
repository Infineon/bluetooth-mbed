# Cypress WICED BT/BLE Host Stack solution (for mbed)

## Overview
Cypress WICED BT/BLE host stack solution includes bluetooth stack library,
bluetooth controller firmware and platform/os porting layer. Bluetooth stack library
is designed for embedded device, it consumes less RAM/ROM usage but still keeps
high performance. With WICED Bluetooth API set, application developers can use them
easily to create their own application. The porting layer is implemented by CYHAL and CY_RTOS_AL
(Cypress Adaptation Layer), hence it can adapt to Cypress platforms, and easy to 
port to other vendor's platform.

## Platform HCI transport config
Besides of stack settings, HCI configuration is also required to specify, 
including pins, format and UART baudrate. Please refer to cybt_platform_config.h 
for more detail:

*  structure **cybt_platform_config_t**
*  API **cybt_platform_config_init( )**
  
The API **cybt_platform_config_init( )** shall be invoked prior to 
**wiced_bt_stack_init( )**

## Specific for mbed
Since Cordio is the default BLE stack in mbed, WICED BT solution is provided as 
alternative option for Cypress platforms. If the developer would like to use 
WICED BT solution, please follow the below modification in mbed_app.json of 
the application in order to disable native Cordio stack, and enable WICED BLE stack.  

Add settings in "target_overrides" configuration  
"{target name}": {  
            "target.extra_labels_remove": ["CORDIO"],  
            "target.features_remove": ["BLE"],
            "target.components_add": ["WICED_BLE"]			
        },  
  
For example, the target is CY8CPROTO_062_4343W  
"target_overrides": {  
		"CY8CPROTO_062_4343W": {  
            "target.extra_labels_remove": ["CORDIO"],   
            "target.features_remove": ["BLE"],
            "target.components_add": ["WICED_BLE"]			
        },  
    }  
    
    
© Cypress Semiconductor Corporation, 2020.