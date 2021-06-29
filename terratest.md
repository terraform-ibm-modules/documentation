Execute the following command to run the testcase on your local machine

``` bash
cd test
```

``` bash
go test -v -timeout 15m -run <test_function_name>
```

If you encounter package dependancy issues while running the above command, please run the following

``` bash
cd ../.. && go mod init
```

``` bash
go mod tidy
```