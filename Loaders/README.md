# Loaders

Loaders are the recommended way of loading data from data sources. 

### Issues with Data Loading tasks in Activities/Fragments 

* Data loading tasks in Activities/Fragments could potentially take longer on an application's main thread resulting in an ANR message.
* When performing data loading tasks in Activities/Fragments, the tasks have to be programmed in accordance with the life cycle events of the Activities and Fragments. 
	A programmer must take into consideration the life cycle events that would occur when an Activity is restarted due to a configuration change, or is destroyed by the system 
	to reclaim memory or is partially obscured.

### Predecessors

Managed Cursors were used prior to the introduction of Loaders in Android 3.0/API 11.

### How Loaders Help

Loaders simplify the process of loading data in an activity or a fragment asynchronously. 

* Loaders handle the ANR problem by performing the data loading tasks on worker threads
* Activities/Fragments can implement callbacks to handle various events related to data loading tasks. 

### Loaders: Key Points

* An Activity/Fragment can be associated with multiple Loaders, each associated with its own data source. 
* A Loader monitors its data source for changes and provides the data updates back to the Activity or Fragment it is associated with.
* Loaders are not destroyed and reconstructed on configuration changes, which eliminates the need for requerying the dataset after configuration changes.
* Loaders can pause data access
* Loaders associated with an Activity/Fragment understand the component's lifecycle events through the component's LoaderManager.
* The interaction between the LoaderManager and the Loaders registered with it occur on the main thread.
* Custom loaders can be implemented by "implementing" the Loader API. Typically, loaders implement AsyncTaskLoader which implements the Loader API asynchronously to run on a worker thread.
* The SDK offers predefined Loaders. For example, a CursorLoader -> AsyncTaskLoader -> Loader, is defined to load cursors from Content Providers.

### LoaderManager: Key Points

The LoaderManager inherent to an Activity generates events that the Activity handles in its callback implementations by implementing *LoaderManager.LoaderCallbacks*. 
These events are generated to:

* Allow an Activity/Fragment to create and initialize loaders
* Notify an Activity/Fragment when the loader finishes loading data. With a Loader of type AsyncTaskLoader, the LoaderManager is notified when the worker thread returns after loading data. 
	The LoaderManager then invokes a callback on the Activity/Fragment to notify that the data is available.
* Allow an Activity/Fragment to close the resource just before the loader is destroyed when the component has to be taken down. 

![](_misc/High%20Level%20Block%20Diagram.png)

### Using loaders in Activities/Fragments

An Activity/Fragment uses a *LoaderManager* object to manage the loaders associated with it. 

* The loaders that have to be used with an Activity/Fragment have to be first registered with the LoaderManager.
* The Activity/Fragment 

