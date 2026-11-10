# Честный знак eps в csv

# Windows

## Нужные программы
```
ImageMagick-7.1.2-33-Q8-x86-dll.exe
gs10080w32.exe
dmtxread.exe
```

## Порядок действий
1. распаковать все eps в каталог
2. перевести все eps в bmp
```sh
for %i in (*.eps) do gswin32c -q -dNOPAUSE -dBATCH -dEPSCrop -sDEVICE=bmpmono -r300 -sOutputFile="%~ni.bmp" "%i"
```
3. распознать каждый bmp файл в текст
```sh
for %i in (*.bmp) do dmtxread -n "%i" >>out.txt
```
4. на всякий случай очистить дубликаты в текстовом файле
```sh
gawk.exe "!seen[$0]++" out.txt > clean.txt
```


# Linux

## Нужные программы
```
sudo apt update
sudo apt install dmtx-utils
sudo apt install ghostscript
```

## Порядок действий
1. распаковать все eps в каталог
2. перевести все eps в bmp
```sh
gs -dSAFER -dBATCH -dNOPAUSE -sDEVICE=bmpmono -r300 -dEPSCrop -sOutputFile=out%d.bmp *.eps;
```
3. распознать каждый bmp файл в текст
```sh
for filename in *.bmp; do	
    dmtxread -n $filename >> out.txt;
done
```
4. на всякий случай очистить дубликаты в текстовом файле
```sh
awk -i inplace '!seen[$0]++' out.txt
```
