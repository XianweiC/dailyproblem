# 关于`conda`在fish报错的修改

文件：`/home/minicinda/bin/activate`

```shell
#!/bin/sh
_CONDA_ROOT="/home/xianwei/miniconda3"
# Copyright (C) 2012 Anaconda, Inc
# SPDX-License-Identifier: BSD-3-Clause
\. "$_CONDA_ROOT/etc/profile.d/conda.sh" || return $?
conda activate "$@"
```

```shell
~/miniconda3/bin/activate (line 2): Unsupported use of '='. In fish, please use 'set _CONDA_ROOT "/home/xianwei/miniconda3"'.
from sourcing file ~/miniconda3/bin/activate
        called on line 185 of file /usr/share/fish/config.fish
in function '.' with arguments '/home/xianwei/miniconda3/bin/activate'
        called on line 29 of file ~/toolbox/apps/PyCharm-P/ch-0/203.6682.86/plugins/terminal/fish/config.fish
from sourcing file ~/toolbox/apps/PyCharm-P/ch-0/203.6682.86/plugins/terminal/fish/config.fish
        called during startup
source：读取文件 “/home/xianwei/miniconda3/bin/activate” 时发生错误
```

## 按照提示修改过后,依然报错

```shell
#!/bin/sh
set _CONDA_ROOT "/home/xianwei/miniconda3"
# Copyright (C) 2012 Anaconda, Inc
# SPDX-License-Identifier: BSD-3-Clause
#\. "$_CONDA_ROOT/etc/profile.d/conda.sh" || return $?
conda activate "$@"
```

## 将第五行注释掉，不再报错，但很慌

```shell
#!/bin/sh
set _CONDA_ROOT "/home/xianwei/miniconda3"
# Copyright (C) 2012 Anaconda, Inc
# SPDX-License-Identifier: BSD-3-Clause
#\. "$_CONDA_ROOT/etc/profile.d/conda.sh" || return $?
conda activate "$argv"
```

