# Running Terratest.

Execute the following command to run the Terratest cases on your local machine.

```bash
cd test
```

```bash
go test -v -timeout 15m -run <test_function_name>
```

If you encounter package dependency issues when you run the previous command, run the following commands:

```bash
cd ../.. && go mod init
```

```bash
go mod tidy
```
