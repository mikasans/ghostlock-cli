# ghostlock-cli

ghostlock 原生 CLI 的构建产物 + Pico 4 Ultra 的内核 profile，做成可直接下载的 release。
构建/发行镜像仓，由 Multica LAB-922 管理。

## 内容

| 文件 | 说明 |
|---|---|
| `ghostlock` | aarch64 Android ELF，ghostlock 的原生命令行（`--load-prebuilt-profile` 等） |
| `5.10.198-perf-*.bin` | 四份 Pico 4 Ultra 内核 profile（GLK1），按 PICO OS 版本 |
| `SHA256SUMS.txt` | 校验和 |

## 用法

```sh
adb push ghostlock /data/local/tmp/ghostlock
adb push 5.10.198-perf-<release>.bin /data/local/tmp/profile.bin
adb shell chmod 755 /data/local/tmp/ghostlock
adb shell /data/local/tmp/ghostlock --load-prebuilt-profile /data/local/tmp/profile.bin
```

`adb/shell` 没有 seccomp 过滤，会跳过 W3，适合先验证。

## 版本对应

| PICO OS | 内核 release（= `uname -r`） |
|---|---|
| 5.13.3 | `5.10.198-perf-g997c65bd51c1-ab1` |
| 5.14.5 | `5.10.198-perf-g42dfb9e97e02-ab1` |
| 5.15.4 | `5.10.198-perf-g9f520a4e4b71-ab1` |
| 5.15.7 | `5.10.198-perf-g49587cd7a509-ab115` |

## 来源与许可

上游 ghostlock-app（Apache-2.0）：https://github.com/YuKongA/ghostlock-app
本仓为其构建产物的镜像，另含我们自己的 Pico profile 适配。

## 注意

这是一个临时提权（root）工具，仅在你自己的设备上用。
