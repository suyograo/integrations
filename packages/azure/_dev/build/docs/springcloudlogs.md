## Azure Spring Cloud Logs

The Azure Spring Cloud Logs integration provides system and application information for Azure Spring Cloud resources.

There are several requirements before using the integration since the logs will have to be read from an azure event hub.

   * the logs have to be exported first to the event hub https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create-kafka-enabled
   * to export activity logs to event hubs users can follow the steps here https://docs.microsoft.com/en-us/azure/azure-monitor/platform/activity-log-export
   * to export audit and sign-in logs to event hubs users can follow the steps here https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub

Users opting for Elastic Cloud native Azure integration can stream the Azure Spring Cloud logs directly to their partner solution clusters, more information and steps can be found here https://www.elastic.co/guide/en/observability/current/monitor-azure.html

### Credentials

`eventhub` :
  _string_
Is the fully managed, real-time data ingestion service.
Default value `insights-operational-logs`.

`consumer_group` :
_string_
 The publish/subscribe mechanism of Event Hubs is enabled through consumer groups. A consumer group is a view (state, position, or offset) of an entire event hub. Consumer groups enable multiple consuming applications to each have a separate view of the event stream, and to read the stream independently at their own pace and with their own offsets.
Default value: `$Default`

`connection_string` :
_string_
The connection string required to communicate with Event Hubs, steps here https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string.

A Blob Storage account is required in order to store/retrieve/update the offset or state of the eventhub messages. This means that after stopping the filebeat azure module it can start back up at the spot that it stopped processing messages.

`storage_account` :
_string_
The name of the storage account the state/offsets will be stored and updated.

`storage_account_key` :
_string_
The storage account key, this key will be used to authorize access to data in your storage account.

`resource_manager_endpoint` :
_string_
Optional, by default we are using the azure public environment, to override, users can provide a specific resource manager endpoint in order to use a different azure environment.
Ex:
https://management.chinacloudapi.cn/ for azure ChinaCloud
https://management.microsoftazure.de/ for azure GermanCloud
https://management.azure.com/ for azure PublicCloud
https://management.usgovcloudapi.net/ for azure USGovernmentCloud
Users can also use this in case of a Hybrid Cloud model, where one may define their own endpoints.


### springcloudlogs

This is the `springcloudlogs` data stream of the Azure Logs package. It will collect any Spring Cloud logs that have been streamed through an azure event hub.

{{event "springcloudlogs"}}

{{fields "springcloudlogs"}}