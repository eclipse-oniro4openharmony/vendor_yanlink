# vendor_hihope

## Introduction

This repository hosts HiHope products: the Neptune series and the DAYU series OpenHarmony smart hardware.

## Directory

```
vendor/hihope
├── neptune_iotlink_demo                  # Neptune100 development board
├── rk3568                                # DAYU200 development board
└── dayu210                               # DAYU210 development board
```

## Creating a New Product Project

Taking the Neptune development board as an example, users can copy the "neptune_iotlink_demo" sample, then tailor or modify it to create their own product project. The following example illustrates how to create a new project.

#### Creating a New Product Project

1. Copy "neptune_iotlink_demo" from the vendor/hihope directory to the same level, and rename it to your product project name (e.g., xxx_iotlink_demo).

2. Enter the xxx_iotlink_demo directory, edit the config.json file, and modify product_name and product_adapter_dir:

```
"product_name": "xxx_iotlink_demo"
"product_adapter_dir": "//vendor/hihope/xxx_iotlink_demo/hals"
```

3. In config.json, you can delete xts, kv_store, and the file management subsystem, retaining necessary subsystems such as kernel, startup, hiviewdfx, and distributedschedule. The following code segments can be removed:
```
"bin_list": [
      {
        "elf_name": "hihope",
        "enable": "true",
        "force_link_libs": [
          "bootstrap",
          "broadcast",
          "hctest",
          "module_ActsParameterTest",
          "module_ActsBootstrapTest",
          "module_ActsDfxFuncTest",
          "module_ActsHieventLiteTest",
          "module_ActsSamgrTest",
          "module_ActsUtilsFileTest",
          "module_ActsKvStoreTest"
        ]
      }
    ],

...

{
  "subsystem": "utils",
  "components": [
    {
      "component": "kv_store",
      "features": [
        "enable_ohos_utils_native_lite_kv_store_use_posix_kv_api = true"
        ]
    },
    { "component": "file", "features":[] }
  ]
},
{
  "subsystem": "xts",
  "components": [
    {
      "component": "xts_acts",
      "features":
        [
          "config_ohos_xts_acts_utils_lite_kv_store_data_path = \"/data\"",
          "enable_ohos_test_xts_acts_use_thirdparty_lwip = true"
        ]
    },
    { "component": "xts_tools", "features":[] }
  ]
}
```

4. Edit "xxx_iotlink_demo/BUILD.gn", group name:
```
group("xxx_iotlink_demo") {
}
```

5. In the root directory of the OpenHarmony source code, execute hb set. The newly added project name "xxx_iotlink_demo" will appear:
```
hihope
   neptune_iotlink_demo
 > xxx_iotlink_demo
```

At this point, a simple product project is set up. Users can follow this method to build their own product projects.

For detailed product compilation and build adaptation procedures, please refer to [Compilation and Build Adaptation Process](https://gitee.com/openharmony/docs/blob/master/en/device-dev/subsystems/subsys-build-product.md)

## Contribution

[How to Participate](https://gitee.com/openharmony/docs/blob/HEAD/en/contribute/contribution-guide.md)

[Commit Message Specification](https://gitee.com/openharmony/device_qemu/wikis/Commit%20message%E8%A7%84%E8%8C%83?sort_id=4042860)

## Related Repositories

* [device/board/hihope](https://gitee.com/openharmony/device_board_hihope)
* [device/soc/winnermicro](https://gitee.com/openharmony/device_soc_winnermicro)
* [device/soc/rockchip](https://gitee.com/openharmony/device_soc_rockchip)