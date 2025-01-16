

---

## **`tar` 命令用法大全**

`tar` 是一个用于创建、查看和解压归档文件的命令行工具。它通常用于处理 `.tar`、`.tar.gz`、`.tgz`、`.tar.bz2` 等格式的文件。

---

### **基本语法**
```bash
tar [选项] [文件或目录]
```

---

### **常用选项**

#### **1. 创建归档文件**
- **`-c`**：创建新的归档文件。
- **`-f`**：指定归档文件的名称。
- **`-v`**：显示操作过程（可选）。
- **`-z`**：使用 gzip 压缩（生成 `.tar.gz` 或 `.tgz` 文件）。
- **`-j`**：使用 bzip2 压缩（生成 `.tar.bz2` 文件）。
- **`-J`**：使用 xz 压缩（生成 `.tar.xz` 文件）。

**示例**：
```bash
# 创建 .tar 归档文件
tar -cvf archive.tar file1 file2 dir1

# 创建 .tar.gz 归档文件
tar -czvf archive.tar.gz file1 file2 dir1

# 创建 .tar.bz2 归档文件
tar -cjvf archive.tar.bz2 file1 file2 dir1

# 创建 .tar.xz 归档文件
tar -cJvf archive.tar.xz file1 file2 dir1
```

---

#### **2. 查看归档文件内容**
- **`-t`**：列出归档文件的内容。
- **`-f`**：指定归档文件的名称。
- **`-v`**：显示详细信息（可选）。

**示例**：
```bash
# 查看 .tar 文件内容
tar -tvf archive.tar

# 查看 .tar.gz 文件内容
tar -tzvf archive.tar.gz

# 查看 .tar.bz2 文件内容
tar -tjvf archive.tar.bz2

# 查看 .tar.xz 文件内容
tar -tJvf archive.tar.xz
```

---

#### **3. 解压归档文件**
- **`-x`**：解压归档文件。
- **`-f`**：指定归档文件的名称。
- **`-v`**：显示操作过程（可选）。
- **`-z`**：解压 gzip 压缩文件（`.tar.gz` 或 `.tgz`）。
- **`-j`**：解压 bzip2 压缩文件（`.tar.bz2`）。
- **`-J`**：解压 xz 压缩文件（`.tar.xz`）。
- **`-C`**：解压到指定目录。

**示例**：
```bash
# 解压 .tar 文件
tar -xvf archive.tar

# 解压 .tar.gz 文件
tar -xzvf archive.tar.gz

# 解压 .tar.bz2 文件
tar -xjvf archive.tar.bz2

# 解压 .tar.xz 文件
tar -xJvf archive.tar.xz

# 解压到指定目录
tar -xzvf archive.tar.gz -C /path/to/directory
```

---

#### **4. 其他常用选项**
- **`--exclude`**：排除指定文件或目录。
- **`--wildcards`**：使用通配符匹配文件。
- **`--strip-components=N`**：解压时去除前 N 层目录。
- **`--overwrite`**：覆盖已存在的文件。
- **`--keep-old-files`**：不覆盖已存在的文件。

**示例**：
```bash
# 排除特定文件
tar -czvf archive.tar.gz --exclude='file1' dir1

# 使用通配符匹配文件
tar -czvf archive.tar.gz --wildcards '*.txt'

# 解压时去除前 1 层目录
tar -xzvf archive.tar.gz --strip-components=1

# 覆盖已存在的文件
tar -xzvf archive.tar.gz --overwrite

# 不覆盖已存在的文件
tar -xzvf archive.tar.gz --keep-old-files
```

---

### **高级用法**

#### **1. 增量备份**
- **`-g`**：创建增量备份。
- **`--listed-incremental`**：指定增量备份的快照文件。

**示例**：
```bash
# 创建增量备份
tar -czvf backup_full.tar.gz -g snapshot.file dir1

# 创建增量备份（基于之前的快照）
tar -czvf backup_incremental.tar.gz -g snapshot.file dir1
```

---

#### **2. 分卷压缩**
- **`--tape-length`**：指定每个分卷的大小（单位：字节）。
- **`-M`**：创建多卷归档文件。

**示例**：
```bash
# 创建分卷压缩文件（每卷 100MB）
tar -czvf - dir1 | split -b 100M - archive_part.tar.gz

# 解压分卷压缩文件
cat archive_part.tar.gz.* | tar -xzvf -
```

---

#### **3. 保留文件属性**
- **`-p`**：保留文件的权限和属性。

**示例**：
```bash
# 创建归档文件并保留文件属性
tar -czvpf archive.tar.gz dir1

# 解压归档文件并保留文件属性
tar -xzvpf archive.tar.gz
```

---

### **总结**

| 选项                 | 描述                  |
| -------------------- | --------------------- |
| `-c`                 | 创建归档文件          |
| `-x`                 | 解压归档文件          |
| `-t`                 | 查看归档文件内容      |
| `-f`                 | 指定归档文件名        |
| `-v`                 | 显示操作过程          |
| `-z`                 | 使用 gzip 压缩/解压   |
| `-j`                 | 使用 bzip2 压缩/解压  |
| `-J`                 | 使用 xz 压缩/解压     |
| `-C`                 | 解压到指定目录        |
| `--exclude`          | 排除指定文件或目录    |
| `--wildcards`        | 使用通配符匹配文件    |
| `--strip-components` | 解压时去除前 N 层目录 |
| `-p`                 | 保留文件属性          |

---

### **常用命令速查表**

| 操作                 | 命令                                             |
| -------------------- | ------------------------------------------------ |
| 创建 `.tar` 文件     | `tar -cvf archive.tar file1 file2 dir1`          |
| 创建 `.tar.gz` 文件  | `tar -czvf archive.tar.gz file1 file2 dir1`      |
| 创建 `.tar.bz2` 文件 | `tar -cjvf archive.tar.bz2 file1 file2 dir1`     |
| 查看 `.tar` 文件内容 | `tar -tvf archive.tar`                           |
| 解压 `.tar.gz` 文件  | `tar -xzvf archive.tar.gz`                       |
| 解压到指定目录       | `tar -xzvf archive.tar.gz -C /path/to/directory` |

---

希望这些内容对你有帮助！如果需要进一步补充或调整，可以随时告诉我！