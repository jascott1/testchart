# Test Charts

Misc charts for ad-hoc testing and examples

## Conditional

Add an optional field "condition" to chart.yaml and requirements.yaml entries. The value of this field would be a YAML path in dot notation (e.g. glance.enabled). The YAML path is then looked up in the parent charts values and if found with a value of false (actual false, not just falsy) the relevant chart is not loaded. If the path does not exist or is not explicitly false, the chart is loaded as normal. 

````
	# parent/values.yaml

	subchart1:
	  enabled: false

````

````
	# parent/requirements.yaml

	dependencies:
	  - name: subchart1
	    repository: http://localhost:10191
	    version: 0.1.0
	    condition: subchart1.enabled

````

In the above example, the chart 'subchart1' would NOT be loaded since its condition value exists in the parent's values and returns false.
See [condition-req](https://github.com/jascott1/testchart/tree/master/condition-req) folder for an example.


