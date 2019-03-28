安装
====
安装配置
最低配置需求：
PlantCV 在以下系统已测试:

Linux: CentOS 7 (RedHat Enterprise Linux)
Linux: Ubuntu 12.04, 14.04, and 16.04
Linux: Raspbian "Jessie"
Mac OSX 10.11 and macOS 10.12+
Windows 10
Cloud9 IDE
需要的依赖包：
Python ( 2.7, 3.6及3.7版本已测试)
argparse
cv2 (即 OpenCV ; 部分功能要求 3.0+ 版本, 推荐使用 3.3+ 版本. 通过 PyPI 的 opencv-python 包进行安装)
matplotlib (最低需求 1.5版, 2+版本可正常工作)
numpy (最低需求 1.11版)
pandas
python-dateutil
scikit-image
scipy
plotnine
setuptools
pytest (仅用于测试)
推荐可选项：
conda (Anaconda 或者 Miniconda)
git
Jupyter
SQLite
通过package管理器安装
PlantCV 的稳定版可以通过 Python 包索引(PyPI)或者通过 Bioconda channel 进行 conda 安装。我们计划至少以月为周期在以上平台发布新版本。

PyPI
在任意虚拟运行环境通过 PyP I安装，以管理员身份或者 --user 角色输入以下内容

pip install plantcv
Conda
初次配制使用 conda 首先需要安装 Anaconda 或 Miniconda 。如有需要，请添加以下通道到conda 配置中。

conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
然后创建环境并安装PlantCV。

conda create -n plantcv plantcv
或者在已有环境中安装PlantCV。

conda install plantcv
手动安装
如果是开发者或者希望最新版本，也可以通过 Github 源安装。

基于 Conda 安装步骤
系统: Linux, macOS, Windows

根据使用情况可以有多种安装选项。如果有系统管理经验可以通过系统 package 管理工具和管理员权限来安装 PlantCV 及其依赖包。(如果安装出现问题可以咨询 )

对大部分用户我们推荐使用跨平台 package 管理系统 conda 进行安装。 Anaconda 或者 Miniconda 编译器都可以进行 conda 。 以下是安装步骤：

下载并安装适用操作系统的  conda 版本。除非有其他原因，我们推荐使用 Python 3。PlantCV 适用于 Python 2.7 但最终会停止针对 2.7 版本的更新。

从 GitHub 下载 PlantCV。可以使用 GitHub 客户端 或者命令行 git 。Git 允许你从 GitHub 更新, 如果不喜欢使用git也可以从 GitHub下载zip压缩包文件。

为 PlantCV 创建包含依赖包的 Python 环境。

安装 OpenCV 和 PlantC。

conda 以及 git 或者 Github 客户端安装完成后，复刻 PlantCV 库，打开命令行终端应用程序（在 Windows 中有其他的选项，本教程中使用 Anaconda Prompt 程序）。以下示例中我们使用 PlantCV 中的环境配置文件。

# 如果不使用Github 客户端程序，通过以下复刻 PlantCV。
git clone https://github.com/danforthcenter/plantcv.git
# 进入 PlantCV 路径 (如果使用Github 客户端程序，以下路径会有所不同)
cd plantcv
# 创建 conda 环境，命名为 "plantcv"  并自动安装依赖包
conda env create -n plantcv -f environment.yml
# 激活 plantcv 环境 (每次开始新任务时都需要)
source activate plantcv
# 测试 PlantCV (可选)
python setup.py test
# 安装 PlantCV
python setup.py install
如果有损坏的环境，可以移除并重复以上步骤。

# 移除环境
conda env remove -n plantcv
sqlite3 在 macOS 和 Linux 版本上已经标配。在 Windows 中可以用 conda 来安装可选项 sqlite3 包.

conda install -c blaze sqlite3
使用 PlantCV 容器
平台: Linux, macOS, Windows

PlantCV 目前支持 Docker 系统，但是对 Singularity 及其他系统的支持还在开发中。 Docker 是一家提供操作系统级别虚拟器的平台。详见 Wikipedia 了解更多背景。容器是一种有效的方式，创建庆良便携的虚拟环境来隔离应用和包。PlantCV Docker 容器可以从 Docker Hub 获取。要使用 PlantCV container 必须要有 本地操作系统安装的 Docker。如果已有 docker， 可以通过以下方式使用 PlantCV :

# 从 Docker Hub 获取最新 PlantCV 镜像
docker pull danforthcenter/plantcv
# 以下简单指令来部署 (导入成功无返回信息)
docker run danforthcenter/plantcv python -c 'import plantcv'
通过PlantCV Docker 容器分析数据需要映射包含容器文件系统的本地文件夹。我们在 /data的容器中设置了一个目录，以便将数据导入/导出容器。 在下面的示例中，本地数据和脚本位于名为/home/user的目录中，但它可以是您想要的任何目录。 /home/user 中的所有内容都可以在容器中访问，写入/容器中的数据的任何输出都将在你提供的本地路径写入。

这种情况下的示例，假设 /home/user 包含一个名为 test-script.py 的 PlantCV 脚本和一个名为 test-image.png 的图像。 在这种情况下，test-script.py 将是一个类似于 VIS tutorial 中描述的脚本。

# 使用 PlantCV docker 图像分析数据
docker run -v /home/user:/data danforthcenter/plantcv \
python /data/test-script.py -i /data/test-image.png -o /data -r /data/plantcv-results.txt
基于脚本的安装
平台: Ubuntu, macOS

复制 PlantCV 库:

git clone https://github.com/danforthcenter/plantcv.git
运行以下配置脚本:

cd plantcv
bash scripts/setup.sh
该脚本将指导你完成安装步骤，成功完成后以使用报告结束。

该脚本已在Ubuntu x86_64位16_04服务器版，OSX 10.11和macOS 10.12上进行了测试。

在其他系统上安装
Cloud9 IDE
Cloud9 是基于云的开发环境，可与Chromebook或其他客户端配合使用。 IDE工作区由Web浏览器中的Docker Ubuntu容器提供支持。

注册帐户后，创建一个新工作区并选择一个Python模板。

安装更新

sudo apt-get update
安装软件依赖包

sudo apt-get install git libopencv-dev python-opencv python-numpy python-matplotlib sqlite3
复制 PlantCV 到主路径

git clone https://github.com/danforthcenter/plantcv.git
默认分支（主）是最新版本。 如果想查看特定版本：

# 切换到稳定版
cd plantcv
git checkout v1.1
安装 PlantCV

sudo python setup.py install

安装完成后进行以下测试：

python -c 'import plantcv'
会返回以下错误:

libdc1394 error: Failed to initialize libdc1394
libdc1394允许程序与在ieee1394标准（火线）上工作的摄像机连接。 由于无法在Cloud9工作空间中启用USB访问，因此在运行管道时将始终出现此错误。 此错误对管道输出没有影响，并且可以继续工作，即使有警告。

要暂时删除驱动程序及错误可以使用：

sudo ln /dev/null /dev/raw1394
再次测试导入，您应该看不到更多错误。 重新启动工作空间将需要再次输入以删除libdc1394错误。

python -c 'import plantcv'
