# Device Tree Visualizer

## requirements

1. python3 -m pip install -r requirements.txt
2. cpp
3. dtc or [patched dtc](https://github.com/bmx666/dtc)

Patched dtc version add extra annotate flags:
* show full list of sources for properties
* prepend comment "/\* \_\_\[|\>\*DELETED\*\<|\]\_\_ \*/" for deleted nodes, labels or properties and comment out them all
* mark all childs of deleted nodes as deleted and do not remove childs

## config file - dtv.conf

* set your preferred editor in env `editor_cmd`
* include extra dts paths into list `include_dir_stubs`

## overlays

### Linux

```
/ {
  fragment@0 {
    target = <&some_node>;
      __overlay__ {
        some_prop = "okay";
        ...
      };
  };
};
```

*TBD: automatically apply overlays*

### Android

Google strongly recommends you do not use `fragment@x` and syntax `__overlay__`, and instead use the reference syntax. For example:

```
&some_node {
  some_prop = "okay";
  ...
};
```

#### Solution for display final overlays

Include base and overlays into temporary dts-file and remove from overlays `/dts-v1/;` and `/plugin/;`

```
#include "base.dts"
#include "overlay1.dts"
#include "overlay2.dts"
```

*TBD: automatically generate temporary file*

[See more](https://source.android.com/devices/architecture/dto/syntax)
