cfDNA-kit
=======================================

Introduction
------------
**cfDNA-kit** is a software use to detect cfDNA feature using WPS signal.

Require：
```angular2html
python2.7
bx-python=0.7.4
pysam=0.7.6
scipy=1.2.3
```

```angular2html
python3.8
yaml
pickle
numpy
matplotlib
sklearn
scipy
seaborn
pandas
tqdm
```

Install
------------
```
git clone https://github.com/lysovosyl/cfDNA-kit.git
cd cfDNA-kit
conda create -n cfDNA-kit python==3.8
conda activate cfDNA-kit
pip install yaml pickle tqdm numpy matplotlib sklearn scipy seaborn pandas

conda create -n wps-kit python==2.7
conda activate wps-kit
pip install bx-python pysam scipy
conda install r-base
```
After you install those software, you should modify those software path in config file, including ./config/config.yaml and ./prepare_bam/test/config.txt

Usage
------------

Step by step
-----------------
Fq to bam

1. First you should build a sample file (samples.lst), just like ./prepare_bam/test/samples.lst 
2. Create a new folder and ensure that samples.lst and config.txt are located in the same folder.
3. Note! You should make sure the softwares in config.txt have been installed and the path of those softwares are correct.
3. Run command.
```
perl ./prepare_bam/bin/prepare_cfdna_bam.pl config.txt
cd out/[sample_name]
make
```
Analyse WPS signal of cfDNA
1. You should build a sample file (sample.lst), just like ./sample.lst
2. This file including four rows, [group_name,group_type,file_name,bam_path]
3. Run command.
```
python ./makeshell.py -sample_file ./your_path/sample.lst -save_dir /your_save_path -tmp_dir /your_temp_path -shell_path /your_shell_path -config ./config/config.yaml -thread 70
```
4. You will get two shell files in your_save_path, including preprocess.sh and summary.sh
5. Then run that two shell files, you should run preprocess.sh at first
```angular2html
cd /your_save_path
sh preprocess.sh && sh summary.sh
```
