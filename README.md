# eps2csv
Честный знак eps в csv


# Нужные программы
`
ImageMagick-7.1.2-33-Q8-x86-dll.exe
gs10080w32.exe
dmtxread.exe
`


1. распаковать все eps  в каталог
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