# Config

## 對下設備設定點位列表

參數說明:

- __cmd__ [ *string* ]

  命令名稱。先前設定是唯一值 ModbusConfig

- __PropertyInit__ [ *object list* ]

  設定介面、鮑率、埠號、裝置列表

  - __interface__ [ *string* ]

    設定介面

  - __Baudrate__ [ *string* ]

    設定鮑率，分別依順序設定BaudRate、Parity 、DataBits 、StopBits ，並用半形逗號隔開

  - __Port__ [ *string* ]

    設定設備連接到的埠號

  - __DeviceInit__ - [ *object list* ]

    使用到的設備類別的細節設定

    - __DeviceDef__ [ *string* ]

      使用的設備點位表，設定於 __DeviceInit__ 中

    - __DeviceIID__ [ *string* ]

      設備編號

    - __DeviceAddr__ [ *int* ]

      設備位置(modbus slave id)

    - __DeviceType__ [ *string* ]

      裝置型態

- __DeviceInit__ [ *object* ]
  
  所使用到的設備之點位表

  - __設備名稱__ [ *string* ] (名稱可自定義)

    PropertyInit.DeviceInit.DeviceDef 會使用到

    - __info__ [ *object* ]

      設定此設備之基本資訊

      - __Manufacturer__ [ *string* ]

        廠商

      - __Model__ [ *string* ]

        型號

      - __ver__ [ *string* ]

        版本

      - __Delay_ms__ [ *string* ]

        延遲秒數，以毫秒(ms)為單位

    - __點位編號__ [ *object* ]

      依照順序排列，由 **001** 開始

      - __FunCode__ [ *int* ]

        Modbus function code

      - __regType__ [ *string* ]

        資料型態

      - __Name__ [ *string* ]

        點位名稱

      - __Len__ [ *int* ]

        資料長度

      - __Addr__ [ *int* ]

        點位位置

範例:

```JSON
{
    "cmd": "ModbusConfig",
    "PropertyInit": [
        {
            "interface": "RS485",
            "DeviceList": [
                {
                    "DeviceDef": "ablerex_es5000hc.ini",
                    "DeviceIID": "A_001",
                    "DeviceAddr": 1,
                    "DeviceType": "Inverter_ablerex"
                },
                {
                    "DeviceDef": "ablerex_es5000hc.ini",
                    "DeviceIID": "A_002",
                    "DeviceAddr": 2,
                    "DeviceType": "Inverter_ablerex"
                },
                {
                    "DeviceDef": "JDA_pyranometer.ini",
                    "DeviceIID": "A_041",
                    "DeviceAddr": 41,
                    "DeviceType": "Pyranometer_JDA"
                },
                {
                    "DeviceDef": "JDA_thermometer.ini",
                    "DeviceIID": "A_042",
                    "DeviceAddr": 42,
                    "DeviceType": "Thermometer_JDA"
                }
            ],
            "Baudrate": "9600,None,8,1",
            "Port": "ttyS0"
        }
    ],
    "DeviceInit": {
        "JDA_pyranometer.ini": {
            "info": {
                "Model": "Pyranometer",
                "Delay_ms": "50",
                "Manufacturer": "JDA",
                "ver": "1.0"
            },
            "001": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "Solar",
                "Len": 2,
                "Addr": 400007
            }
        },
        "ablerex_es5000hc.ini": {
            "011": {
                "FunCode": 3,
                "regType": "int_be_d10",
                "Name": "ACF1",
                "Len": 2,
                "Addr": 449190
            },
            "026": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "BATDC",
                "Len": 2,
                "Addr": 449205
            },
            "025": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "BATCC",
                "Len": 2,
                "Addr": 449204
            },
            "027": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "BATCP_01",
                "Len": 2,
                "Addr": 449206
            },
            "013": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "DCBNV",
                "Len": 2,
                "Addr": 449192
            },
            "021": {
                "FunCode": 3,
                "regType": "int_be_d100",
                "Name": "IPB_01",
                "Len": 2,
                "Addr": 449200
            },
            "018": {
                "FunCode": 3,
                "regType": "int_be_d10",
                "Name": "DCCL1",
                "Len": 2,
                "Addr": 449197
            },
            "008": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "ACVL1L2",
                "Len": 2,
                "Addr": 449187
            },
            "015": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "IHT",
                "Len": 2,
                "Addr": 449194
            },
            "info": {
                "Model": "ES5000HC",
                "Delay_ms": "50",
                "Manufacturer": "Ablerex",
                "ver": "1.0"
            },
            "012": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "DCBPV",
                "Len": 2,
                "Addr": 449191
            },
            "022": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "TOTALKWH_01",
                "Len": 2,
                "Addr": 449201
            },
            "020": {
                "FunCode": 3,
                "regType": "int_be_d100",
                "Name": "IPA_01",
                "Len": 2,
                "Addr": 449199
            },
            "004": {
                "FunCode": 3,
                "width": 16,
                "Addr": 49168,
                "regType": "be_w2b",
                "Name": "ERRORS_02",
                "Len": 2
            },
            "017": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "DCVL2",
                "Len": 2,
                "Addr": 449196
            },
            "028": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "BATCP_02",
                "Len": 2,
                "Addr": 449207
            },
            "019": {
                "FunCode": 3,
                "regType": "int_be_d10",
                "Name": "DCCL2",
                "Len": 2,
                "Addr": 449198
            },
            "014": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "IIT",
                "Len": 2,
                "Addr": 449193
            },
            "003": {
                "FunCode": 3,
                "width": 16,
                "Addr": 49167,
                "regType": "be_w2b",
                "Name": "ERRORS_01",
                "Len": 2
            },
            "009": {
                "FunCode": 3,
                "regType": "int_be_d10",
                "Name": "ACCL1",
                "Len": 2,
                "Addr": 449188
            },
            "024": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "BATV",
                "Len": 2,
                "Addr": 449203
            },
            "016": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "DCVL1",
                "Len": 2,
                "Addr": 449195
            },
            "002": {
                "FunCode": 3,
                "width": 16,
                "Addr": 49153,
                "regType": "be_w2b",
                "Name": "ALARMS_02",
                "Len": 2
            },
            "005": {
                "FunCode": 3,
                "regType": "int_be_d100",
                "Name": "OPTPWR_01",
                "Len": 2,
                "Addr": 449184
            },
            "023": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "TOTALKWH_02",
                "Len": 2,
                "Addr": 449202
            },
            "006": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "ACV1",
                "Len": 2,
                "Addr": 449185
            },
            "010": {
                "FunCode": 3,
                "regType": "int_be_d10",
                "Name": "ACCL2",
                "Len": 2,
                "Addr": 449189
            },
            "001": {
                "FunCode": 3,
                "width": 16,
                "Addr": 49152,
                "regType": "be_w2b",
                "Name": "ALARMS_01",
                "Len": 2
            },
            "007": {
                "FunCode": 3,
                "regType": "int_be",
                "Name": "ACV2",
                "Len": 2,
                "Addr": 449186
            }
        },
        "JDA_thermometer.ini": {
            "info": {
                "Model": "Thermometer",
                "Delay_ms": "50",
                "Manufacturer": "JDA",
                "ver": "1.0"
            },
            "001": {
                "FunCode": 3,
                "regType": "int_be_d10",
                "Name": "Temp",
                "Len": 2,
                "Addr": 400007
            }
        }
    }
}
```

# Schedule

## 對下設備設定排程列表

參數說明:

- __cmd__ [ *string* ]

  命令名稱。必須設定，先前設定是唯一值 ModbusSchedule

- __token__ [ *string* ]

  回傳權杖，判別用

- __ScheduleIni__ [ *object* ]

  依照使用的埠號區分成不同的 object list

  - __埠號名稱__ [ *object list* ]

    用法是會依照這個陣列的順序下去讀取設備資訊，讀到 **Nulldevice01** 會延遲秒數

    - __設備編號__ [ *string* ]

      固定後面接空字串 ""

    - __Nulldevice01__ [ *string* ]

        延遲秒數

範例:

```JSON
{
    "cmd": "ModbusSchedule",
    "token": "01",
    "ScheduleIni": {
        "ttyS0": [
            {
                "A_001": ""
            },
            {
                "A_002": ""
            }
            {
                "A_041": ""
            },
            {
                "A_042": ""
            },
            {
                "Nulldevice01": "288"
            }
        ]
    }
}
```
