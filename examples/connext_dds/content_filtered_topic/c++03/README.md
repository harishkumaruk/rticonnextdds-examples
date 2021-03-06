# Example Code: Content Filtered Topic

## Building C++03 Example
Before compiling or running the example, make sure the environment variable
`NDDSHOME` is set to the directory where your version of *RTI Connext* is
installed.

Run *rtiddsgen* with the `-example` option and the target architecture of your
choice (e.g., *i86Win32VS2010* or *i86Linux2.6gcc4.4.5*). The *RTI Connext Core
Libraries and Utilities Getting Started Guide* describes this process in detail.
Follow the same procedure to generate the code and build the examples. **Do not
use the `-replace` option.** Assuming you want to generate an example for
*i86Win32VS2010* run:
```
rtiddsgen -language C++03 -example i86Win32VS2010 cft.idl
```

You will see messages that look like this:
```
File C:\local\content_filtered_topic\c++03\cft_subscriber.cxx already exists and
will not be replaced with updated content. If you would like to get a new file
with the new content, either remove this file or supply -replace option.
File C:\local\content_filtered_topic\c++03\cft_publisher.cxx already exists and
will not be replaced with updated content. If you would like to get a new file
with the new content, either remove this file or supply -replace option.
```

This is normal and is only informing you that the subscriber/publisher code has
not been replaced, which is fine since all the source files for the example are
already provided.

## Running C++03 Example
In two separate command prompt windows for the publisher and subscriber. Run
the following commands from the example directory (this is necessary to ensure
the application loads the QoS defined in *USER_QOS_PROFILES.xml*):

On *Windows* systems run:
```
objs\<arch_name>\cft_publisher.exe  <domain_id> <samples_to_send>
objs\<arch_name>\cft_subscriber.exe <domain_id> <sleep_periods> <select_cft>
```

On *UNIX* systems run:
```
./objs/<arch_name>/cft_publisher  <domain_id> <samples_to_send>
./objs/<arch_name>/cft_subscriber <domain_id> <sleep_periods> <select_cft>
```

The applications accept up to three arguments:
    1. The `<domain_id>`. Both applications must use the same domain ID in order
    to communicate. The default is 0.
    2. How long the examples should run, measured in samples for the publisher
    and sleep periods for the subscriber. A value of '0' instructs the
    application to run forever; this is the default.
    3. (subscriber only) The *select Content Filtered Topic* switch. If 1, then
    we use a *Content Filtered Topic*. If 0, then we use a normal *Topic*.
    The default is 1.
