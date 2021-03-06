# oci_core_console_history

## ConsoleHistory Resource

### ConsoleHistory Reference

The following attributes are exported:

* `availability_domain` - The Availability Domain of an instance.  Example: `Uocm:PHX-AD-1` 
* `compartment_id` - The OCID of the compartment.
* `defined_tags` - Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Operations.CostCenter": "42"}` 
* `display_name` - A user-friendly name. Does not have to be unique, and it's changeable. Avoid entering confidential information.  Example: `My console history metadata` 
* `freeform_tags` - Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Department": "Finance"}` 
* `id` - The OCID of the console history metadata object.
* `instance_id` - The OCID of the instance this console history was fetched from.
* `state` - The current state of the console history.
* `time_created` - The date and time the history was created, in the format defined by RFC3339. Example: `2016-08-25T21:10:29.600Z` 



### Create Operation
Captures the most recent serial console data (up to a megabyte) for the
specified instance.

The `CaptureConsoleHistory` operation works with the other console history operations
as described below.

1. Use `CaptureConsoleHistory` to request the capture of up to a megabyte of the
most recent console history. This call returns a `ConsoleHistory`
object. The object will have a state of REQUESTED.
2. Wait for the capture operation to succeed by polling `GetConsoleHistory` with
the identifier of the console history metadata. The state of the
`ConsoleHistory` object will go from REQUESTED to GETTING-HISTORY and
then SUCCEEDED (or FAILED).
3. Use `GetConsoleHistoryContent` to get the actual console history data (not the
metadata).
4. Optionally, use `DeleteConsoleHistory` to delete the console history metadata
and the console history data.


The following arguments are supported:

* `defined_tags` - (Optional) Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Operations.CostCenter": "42"}` 
* `display_name` - (Optional) A user-friendly name. Does not have to be unique, and it's changeable. 
* `freeform_tags` - (Optional) Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Department": "Finance"}` 
* `instance_id` - (Required) The OCID of the instance to get the console history from.


### Update Operation
Updates the specified console history metadata.

The following arguments support updates:
* `defined_tags` - Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Operations.CostCenter": "42"}` 
* `display_name` - A user-friendly name. Does not have to be unique, and it's changeable. 
* `freeform_tags` - Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Department": "Finance"}` 


** IMPORTANT **
Any change to a property that does not support update will force the destruction and recreation of the resource with the new property values

### Example Usage

```hcl
resource "oci_core_console_history" "test_console_history" {
	#Required
	instance_id = "${oci_core_instance.test_instance.id}"

	#Optional
	defined_tags = {"Operations.CostCenter"= "42"}
	display_name = "${var.console_history_display_name}"
	freeform_tags = {"Department"= "Finance"}
}

```

# oci_core_console_histories

## ConsoleHistory DataSource

Gets a list of console_histories.

### List Operation
Lists the console history metadata for the specified compartment or instance.

The following arguments are supported:

* `availability_domain` - (Optional) The name of the Availability Domain.  Example: `Uocm:PHX-AD-1` 
* `compartment_id` - (Required) The OCID of the compartment.
* `instance_id` - (Optional) The OCID of the instance.
* `state` - (Optional) A filter to only return resources that match the given lifecycle state.  The state value is case-insensitive. 


The following attributes are exported:

* `console_histories` - The list of console_histories.

### Example Usage

```hcl
data "oci_core_console_histories" "test_console_histories" {
	#Required
	compartment_id = "${var.compartment_id}"

	#Optional
	availability_domain = "${var.console_history_availability_domain}"
	instance_id = "${oci_core_instance.test_instance.id}"
	state = "${var.console_history_state}"
}
```