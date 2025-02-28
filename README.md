# Support Team Take-Home Assessment Answers

[View Google Doc Version](https://docs.google.com/document/d/154R35DxuTyABwhDU7-_eVlaeRQ4hc-VWCZujx8o8vQo/edit?usp=sharing)

### Section 1:

1. In `_get_sweep_url()`, explain the purpose of the `urllib.parse.quote()` function calls. What is their effect on the URL generation?
   
   The `urllib.parse.quote()` function encodes special characters in entity, project, and sweep_id (e.g., a space becomes %20) to ensure the URL is valid for web requests. This prevents errors from unencoded characters like slashes or spaces.

2. In `sweep()`, describe how the `InternalApi` class is instantiated and used. What is its operation and how does it interact with the API?
   
   The `InternalApi` class is instantiated with `api = InternalApi()` and used in `api.upsert_sweep(sweep, prior_runs=prior_runs)` to create or update a sweep on the Weights & Biases backend. It handles authentication and data serialization, returning a sweep_id.

3. In `controller()`, explain the role of the `_WandbController` class. How does it facilitate sweep control and configuration?
   
   The `_WandbController` class manages sweep configuration and execution. It provides methods like `configure_search()` and `configure_stopping()` to set parameters and properties like `sweep_config` and `sweep_id` for programmatic control, connecting to or creating a sweep.

### Section 2:

4. What is the function of the `_parse_scheduled` method, and what is the significance of the `scheduled_list` variable within this method?
   
   The `_parse_scheduled` method analyzes `scheduled_list`—a list of run entries from the backend—to track scheduled runs' status. It returns lists of started, stopped, and completed runs to sync the controller with the server.

5. How does the `_step` method utilize the results obtained from the `_parse_scheduled` method?
   
   The `_step` method uses `_parse_scheduled` results to update `self._controller`, removing started schedules and stopped/completed runs from schedule and earlystop lists, keeping only pending actions.

6. Within the `_step` method, what is the importance of the `new_schedule_list` and `new_earlystop_list` variables? How do these variables affect the state of the schedule and earlystop entries in the `_controller` dictionary?
   
   `new_schedule_list` and `new_earlystop_list` filter out started schedules and stopped/completed runs, respectively. They update `self._controller` to include only pending actions, avoiding redundant requests.

7. Within the `_sweep_object_read_from_backend` method, what is the role of the `rr` variable and how is it used?
   
   The `rr` variable parses JSON strings (e.g., summaryMetrics, config) into Python objects, creating SweepRun objects from run dictionaries for use in the controller.

8. How does the `_sweep_status` method determine the status of individual sweep runs? Describe the criteria or conditions used to classify a run as stopped or stopping based on the `sweep_runs` list.
   
   The `_sweep_status` method marks a run as stopped if its `stopped` attribute is True and as stopping if `should_stop` is True, based on the `sweep_runs` list.

9. In the `_sweep_status` method, what is the purpose of the `run_type_counts` variable? How is it calculated, and what information does it provide about the different types of runs within the `sweep_runs` list?
   
   The `run_type_counts` variable, calculated by `_get_run_counts`, counts runs by state (e.g., pending, running, finished) in `sweep_runs`. It summarizes the distribution of run states for progress tracking.

---

