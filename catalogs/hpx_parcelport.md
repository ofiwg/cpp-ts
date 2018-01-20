the file hpx_parcelport.csv contains a table cataloging the following
information about the use of libfabric primitives in the hpx runtime.

libfabric-primitive,file,line,description,,

this table includes information about how the hpx runtime uses libfabric in
it's parcelport, or communication, system.

here is a description of the columns:

* libfabric-primitive - contains the name of the type and variable used in hpx
parcelport
* file - the file name containing the libfabric primitive
* line - the line number referencing the libfabric primitive's instantiation
* description - a quick explanation of how the libfabric primitive's instance
is used
