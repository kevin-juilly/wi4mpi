Known limitations
*****************

MPI_MAX_* constants for strings size
====================================

MPI defines constants for the maximum length of some strings. Since their values can be different between the application side and the runtime side, truncation might happen.

This could provoke issues with some routines because the strings might have different values between what the application sees and what the runtime expects.

MPI_MAX_PORT_NAME
-----------------

Because port names are given by the runtime, if truncation happens the application will get a string that won't be usable in functions expecting a port name.

MPI_MAX_INFO_KEY
----------------

Since key-value pairs in an MPI_Info object have a maximum length, truncation of the key might happen when setting one. Thus you could have an MPI_Info object with unexpected behaviour.

MPI_MAX_INFO_VAL
----------------

The MPI standard discourage the allocation of a string with this size, allowing it to be very big. Thus we defer to the runtime the size check.
It means that a value might not be accepted when setting it, even if the application checked that it is less than MPI_MAX_INFO_VAL.

Other constants
---------------

Since other constants are either for information (type, window and communicator's name, processor name and library version string) or with only a portable subset (datarep of file views), their truncation is less at risk of provoking issues in their uses.
