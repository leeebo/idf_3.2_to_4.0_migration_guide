
根据乐鑫  [ESP-IDF 支持期限政策](https://github.com/espressif/esp-idf/blob/master/SUPPORT_POLICY.md)，`V3.2.x`  版本将在 2020 年 10 月停止支持，为了获得更新的特性和更安全的体验，建议版本升级到V4.0 及以后版本。

## 获取版本信息

**编译时获取**

宏定义：

* IDF_VER：字符串，与 `esp_get_idf_version()` 返回一致。例如：`v4.0.1-dirty`
* ESP_IDF_VERSION：int，以编号的标识版本。例如：`262144`
* ESP_IDF_VERSION_MAJOR：int,主版本号
* ESP_IDF_VERSION_MINOR：int,次版本号
* ESP_IDF_VERSION_PATCH：int,补丁编号
* ESP_IDF_VERSION_VAL：将版本号转换成版本编号

使用示例：

```
#include "esp_idf_version.h"

#if ESP_IDF_VERSION >= ESP_IDF_VERSION_VAL(4, 0, 0)
    // enable functionality present in IDF v4.0
#endif
```


**运行时获取**

函数： `const char *esp_get_idf_version(void)`

>需要包含头文件 `esp_common/include/esp_idf_version.h` 或包含 `esp_system.h`

使用示例：

```
#include "esp_idf_version.h"

...

ESP_LOGI(TAG, "[APP] IDF version: %s", esp_get_idf_version());

//输出 IDF version: v4.0.1-dirty
```

>这个函数相比使用宏定义获取版本号，可以获取更多信息，例如显示是否为内测版本 `development`, `pre-release` and `release` versions.

## 外设

### ADC

|项目| v3.2 |v4.0|
|--|--|--|
| 文档 | * | 新增：芯片 [ADC 校准版本信息](https://docs.espressif.com/projects/esp-idf/en/v4.0.1/api-reference/peripherals/adc.html#calibration-values) |
|头文件|soc/adc_channel.h|soc/adc_periph.h|
|API|int adc1_get_voltage(adc1_channel_t channel) | 移除，统一用 int adc1_get_raw(adc1_channel_t channel) |

### I2C

|项目| v3.2 |v4.0|
|--|--|--|
| 文档 | * | 修正：mode 错误描述 |
| API|*  | 相同 |

### LEDC

|项目| v3.2 |v4.0|
|--|--|--|
| 文档 | * | 修正：语法优化 |
| API：类型| ledc_clk_src_t  | 新增类型：ledc_clk_cfg_t ，兼容 ledc_clk_src_t |
| API：结构体| ledc_timer_config_t::bit_num | 移除，统一用 ledc_timer_config_t::duty_resolution |
| API：结构体| * | 新增 ledc_timer_config_t::ledc_clk_cfg_t|
| API：函数| * | 新增  ledc_set_pin  |


* 4.0 ledc 在配置时可通过 `ledc_timer_config_t::ledc_clk_cfg_t` 选择时钟源
* 4.0 ledc 可使用 `ledc_set_pin` 选择 `GPIO`

> 160Khz 最大 8 bits；5 Khz 最大 13 bits 

### SPI master

|项目| v3.2 |v4.0|
|--|--|--|
| 文档 | * | 修正：SPI_USE_RXDATA->SPI_TRANS_USE_RXDATA |
|  API：结构体|*  | 新增：spi_transaction_ext_t::dummy_bits|
|  API：函数|spi_bus_free  | 私有 |
|  API：函数|spi_bus_initialize  | 私有 |

* 4.0 spi 可使用 `spi_get_actual_clock` 可获取实际的 spi 工作频率
* 可设置 `spi_transaction_ext_t::dummy_bits` 发送  dummy byte

### SPI slave



## 系统
### 宏定义
```
/home/libo/esp-iot-solution/tools/unit-test-app/sdkconfig.defaults:11 CONFIG_TASK_WDT was replaced with CONFIG_ESP_TASK_WDT
/home/libo/esp-iot-solution/tools/unit-test-app/sdkconfig.defaults:35 CONFIG_GATTC_ENABLE was replaced with CONFIG_BT_GATTC_ENABLE
/home/libo/esp-iot-solution/tools/unit-test-app/sdkconfig.defaults:36 CONFIG_BLE_SMP_ENABLE was replaced with CONFIG_BT_BLE_SMP_ENABLE
/home/libo/esp-iot-solution/tools/unit-test-app/sdkconfig.defaults:38 CONFIG_BLE_SCAN_DUPLICATE was replaced with CONFIG_BTDM_BLE_SCAN_DUPL
/home/libo/esp-iot-solution/tools/unit-test-app/sdkconfig.defaults:242 CONFIG_ULP_COPROC_ENABLED was replaced with CONFIG_ESP32_ULP_COPROC_ENABLED
/home/libo/esp-iot-solution/tools/unit-test-app/sdkconfig.defaults:243 CONFIG_ULP_COPROC_RESERVE_MEM was replaced with CONFIG_ESP32_ULP_COPROC_RESERVE_MEM
```
