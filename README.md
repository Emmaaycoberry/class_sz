# CLASS_SZ (Mac M1 Compatible Fork)

This repository is a **fork** of the main [`class_sz`](https://github.com/CLASS-SZ/class_sz) project, adapted to allow **installation and compilation on Mac M1**, using the SOlikeT environment, without issues.

### 🔧 What was changed
In the `Makefile`, I modified the `INCLUDES` and `LDFLAGS` variables so they use the **OpenMP**, **FFTW**, and **GSL** libraries installed via **conda** during the installation of SOlikeT.  

If you prefer to install the developer version of `class_sz` **without** the SOlikeT environment, you will need to install **OpenMP**, **FFTW**, and **GSL** either via **conda** (or **Homebrew**, and then adapt the `INCLUDES` and `LDFLAGS` variables accordingly to match your local installation paths).

## 🧩 Prerequisites

You first need to install the **SOlikeT environment**.

- I used this fork: [SOlikeT (master branch)](https://github.com/olakusiak/SOLikeT/tree/master)
- Follow the installation instructions from that repository.

To make the installation work on Mac M1, I locally modified the following files:
- `requirements.txt`: remove pyccl
- `soliket-tests.yml`: add pyccl

➡️ The modification ensures that **`pyccl` is installed via `conda`** instead of `pip`.

## ⚙️ Installation Instructions

Once the SOlikeT environment is created, follow the steps below to install the developer version of `class_sz`, using this fork of the `class_sz` repository.

```bash
git clone https://github.com/Emmaaycoberry/class_sz.git
git clone https://github.com/CLASS-SZ/get_cosmopower_emus.git

cd get_cosmopower_emus
pip install -e .
cd ../

git clone https://github.com/CLASS-SZ/class_sz_data.git
cd class_sz_data
pip install -e .
cd ../

cd class_sz/class-sz/python
git clone https://github.com/CLASS-SZ/classy_szfast
cd ../
```

> **Note:**  
> This fork already includes a Makefile compatible with **Mac M1**, so you don’t need to run the `select_makefile.sh` script, mentioned in the class_sz documentation.  
> ```bash
> ./select_makefile.sh
> ```

``` bash
./download_emulators.sh

export PATH_TO_CLASS_SZ_DATA=$PWD/../class_sz_data_directory

make clean
make -j

cd python/classy_szfast
pip install -e .
cd ../../

export PYTHONPATH=$(pwd)/python/classy_szfast:$PYTHONPATH
```

## ✅ Test the Installation
You should now be able to run class_sz:  
⚠️ It will only work from the class_sz/class-sz folder.

``` bash
$ python
>>> import classy_sz
```

## 🌍 Environment Variables 
To make your setup persistent, create a file called `.class_sz_env.sh` and adapat the `/path/to/class_sz`:  

``` bash
export PATH_TO_CLASS_SZ_DATA=/path/to/class_sz/class_sz_data_directory
export PYTHONPATH=/path/to/class_sz/class-sz/python/classy_szfast:
```
> **Note:**  
> You can check your path using `echo $PATH_TO_CLASS_SZ_DATA` and `echo $PYTHONPATH`.  


Then source it in your terminal:
``` bash
source .class_sz_env.sh
```
