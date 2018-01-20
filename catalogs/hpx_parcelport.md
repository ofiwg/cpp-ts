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

this document will contain a more contextual analysis describing the hpx
parcelport's design and implementation. this document will attempt to provide
a more general perspective, or analysis, that ties together contents included
in the csv file.

file reviewed /plugins/parcelport/libfabric/libfabric_controller.hpp

*** summary of lines 142:176

libfabric_controller::libfabric_controller(
    std::string provider,
    std::string domain,
    std::string endpoint
    int port=7910);

constructor uses a function called open_fabric(provider, domain, endpoint) to
access the hardware.

constructor creates a memory pool object which manages a memory containing 
rma_memory_pool<libfabric_region_provider>(fabric_domain_) data segments.
the constructor also initalizes a passive listener (or an active RDM endpoint)
using the function called create_local_endpoint()

*** summary of lines 315::402

libfabric_controller::open_fabric(
    std::string provider,
    std::string domain,
    std::string endpoint_type);

this method calls fi_allocinfo() and stores results into a local variable called
struct fi_info * fabric_hints_. the method checks to see if fi_allocinfo returns
correctly.

    fabric_hints_->caps is set to FI_MSG|FI_RMA|FI_SOURCE|FI_WRITE
|FI_READ|FI_REMOTE_READ|FI_REMOTE_WRITE|FI_RMA_EVENT

    fabric_hints_->mode is set to FI_CONTEXT|FI_LOCAL_MR

    fabric_hintes_->fabric_attr->prov_name is set to provider.c_str()

    fabric_hints_->domain_attr->name is set to domain.c_str()

    fabric_hints_->domain_attr->mr_mode is set to FI_MR_BASIC (basic IB
    registration)

progress threads are disabled by setting 

    fabric_hints_->domain_attr->control_progress to FI_PROGRESS_MANUAL
    fabric_hints_->domain_attr->data_progress to FI_PROGRESS_MANUAL

thread safe mode is enabled (and notes that this does not work with psm2
provider) by setting

    fabric_hints_->domain_attr->threading to FI_THREAD_SAFE

resource management is enabled by setting

    fabric_hints_->domain_attr->resource_mgmt to FI_RM_ENABLED

shared recv context is enabled for active endpoints

    fabric_hints_->ep_attr->rx_ctx_cnt = FI_SHARED_CONTEXT

if the endpoint_type value is set to "msg" then the following value
is set:

    fabric_hints->ep_attr->type to FI_EP_MSG

if the endpoint_type value is set to "rdm" then the following value
is set:

    fabric_hints->ep_attr->type to FI_EP_RDM

if the endpoint_type value is set to "dgram" then the following value
is set:

    fabric_hints->ep_attr->type to FI_EP_DGRAM

by default, the method wants completions on both tx/rx events and sets

    fabric_hints_->tx_attr->op_flags to FI_COMPLETION
    fabric_hints_->rx_attr->op_flags to FI_COMPLETION

fi_get_info is called and then tests to see if the following values
are set:

    fabric_info_->rx_attr->mode & FI_RX_CQ_DATA != 0
    fabric_hints_->mode & FI_CONTEXT != 0

fi_fabric is called and given the following arguments

    fi_fabric(fabric_into_->fabric_attr, & fabric_, nullptr )

fi_domain is called and given the following arguments

    fi_domain(fabric_, fabric_info_, &fabric_domain_, nullptr)

a method called '_set_disable_registration()' for Cray systems, it
disables memory registration caching.

fi_free_info is called and passed the following arguments

    fi_free_info( fabric_hints_ )


