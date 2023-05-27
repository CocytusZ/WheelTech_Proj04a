# Adb 命令

## 查看日志

### 基础指令

```{.sh}
adb logcat
```

### 标签过滤

```{.sh}
adb logcat -s <TAG>
```

### 层级过滤
```{.sh}
// Error
adb logcat *:E
// Info
adb logcat *:I

// Debug
adb logcat *:D

// Verbose
adb logcat *:V

```