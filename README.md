# dockerfile-pdf-converter

ExcelをPDFに変換したりPDFを結合するためのDocker環境を作成するためのDockerfileです

## docker イメージのビルド

```
$ docker build . -t pdfconverter
```

## hoge.xlsx ファイルを pdfフォルダにPDF形式として変換する

内部的には LibreOffice の soffice コマンドを使っています。

```
$ docker run --rm -v `pwd`:/work -it pdfconverter soffice --headless --nologo --nofirststartwizard  --convert-to pdf --outdir pdf hoge.xlsx
```

## pdfフォルダに存在するPDFファイルを result.pdf に変換

内部的にはPDF Toolkit の pdftk コマンドを使っています。

```
$ docker run --rm -v `pwd`:/work -it pdfconverter pdftk pdf/* cat output result.pdf
```

## TODO

下記のような警告メッセージが出てしまうのを抑止する

```
W: Unknown node under /registry/extlang: deprecated
W: Unknown node under /registry/grandfathered: comments
W: Unknown node under /registry/grandfathered: comments
W: Unknown node under /registry/extlang: deprecated
W: Unknown node under /registry/grandfathered: comments
W: Unknown node under /registry/grandfathered: comments
convert /work/hoge.xlsx -> /work/pdf/hoge.pdf using filter : calc_pdf_Export
Overwriting: /work/pdf/hoge.pdf
```


