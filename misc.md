
全snippetサブフォルダに特定の名前のファイルを作成する。

```sh
NAME=__new_file_name__ # replace here!!
cd snippet
for sample in `find snippet -type f -name "_sample.*"`
do
  cp $sample ${sample%/*}/$NAME.${sample##*.}
done

subl ./snippet/*/$NAME.*
```


