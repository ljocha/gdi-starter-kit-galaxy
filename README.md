# Galaxy in GDI starter kit

This part of the starter kit setup demonstrates the use of Galaxy to process data files available over `htsget`.
A standalone Galaxy runs aside of the other components, in the expected trusted environment, there is no need to download the data elsewhere.

The data are accessed with a custom Galaxy tool, taking the file name and user's authorization token as inputs. Preferably, this download tool should be used as an initial step
of Galaxy workflow configured with `Output cleanup` flag on so that the sensitive file is deleted as soon as it is not needed anymore.
The risk of unintentional disclosure of the sensitive content is minimized in this way.
On the other hand, the setup does not prevent malicious user, once (s)he gets access to it, to download the data by intention; this was not the purporse.

## Running the service

1. start https://github.com/GenomicDataInfrastructure/starter-kit-storage-and-interfaces according to the instructions; _Demo_ mode will work out of the box, use of LS-AAI-mock of full LS AAI would require some tweaking
2. start https://github.com/GenomicDataInfrastructure/starter-kit-htsget according to the instructions on the same machine
3. run `docker-compose up` in a clone of this repo on the same machine; this step starts the Galaxy container and installs the custom tool `gdi_sk` from [test toolshed](https://testtoolshed.g2.bx.psu.edu/)https://testtoolshed.g2.bx.psu.edu/
4. run `docker-compose restart galaxy`; this is required for Galaxy to pick up the tool's dependencies (htsget client) correctly

