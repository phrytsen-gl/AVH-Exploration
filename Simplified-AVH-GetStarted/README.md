# Simplified version of the official [AVH Getting Started Example](https://github.com/ARM-software/AVH-GetStarted)

*NOTE:* To execute the following commands you will need the AVH Toolset to be installed. Or you can provision an AWS
EC2 based on [ARM Virtual Hardware AMI from the AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-urbpq7yo5va7g).

## Build the Test Suite:
Project uses the [CMSIS-Build system](https://open-cmsis-pack.github.io/devtools/buildmgr/latest/index.html).
- Convert the solution file to `.cprj`:
  ```console
  $> csolution convert -s AVH-Example-CMSIS-Build.csolution.yml
  ```
- Translate `.cprj` file to the `CMakeFile.txt` and build the source code to CMSIS-Compatible binary:
  ```console
  $> cbuild --packs SSE-300-MPS3/SSE-300-MPS3.Debug+Board.cprj
  ```

The mentioned above steps will generate `.asx` binary that can be executed on both real target HW and ARM Fixed Virtual Platforms (FVPs).

## Run CMSIS-Compatible binary on ARM Fixed Virtual Platform:
Execute the compiled test suite on the `VHT_Corstone_SSE-300_Ethos-U55` FVP. It's expected that 1 test will be failed.
```console
$> VHT_Corstone_SSE-300_Ethos-U55 --stat --simlimit 1 -f fvp_config.txt out/SSE-300-MPS3/Board/Debug/SSE-300-MPS3.Debug+Board.axf
```
There are two available platforms to run the binary: `VHT_Corstone_SSE-300_Ethos-U55` and `VHT_Corstone_SSE-300_Ethos-U65`.
