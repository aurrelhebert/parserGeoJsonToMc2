## GEOJSON parser to mc2 files

Small python script to generate splitted MC2 macro files. According to the conf files, it generates the working geometry macro, that can be pushed on a Warp10 instance.

Those macro can be used for GEO mapping as example.

# Conf

For each GeoJson files to parse in repository, create a specific JSON object:

```
[
	{
		"filename": "my.geojson",
		"prefix": "tmp/",
		"inside": "false",
		"errorPercentage": "0.001",
		"warpscriptName": "Country",
		"directories": 
		[
			"name"
		]
	}
]
```

The conf used previously will extract for the GEOJSON file given (filename option in conf file), the property of each feature called "name" (directories option in conf file). Then in the repository tmp (prefix option in conf file - the prefix name have to end with a '/'), it will create the associated "name" sub-directory. Several sub-directories can be created, it will kept the same order as given by "directories" list. 
The file generated as output containing the GEO macro will be called Country.mc2 (warpscriptName option in conf file). This will set the specific GEO.JSON parameters using inside (by default true) and errorPercentage (by default 0.1) set in the conf file.

To load the file name accoriding to a property of the feature, you can replace the warpscriptName option by warpscriptLoad.

```
[
	{
		"filename": "my.geojson",
		"prefix": "tmp/",
		"warpscriptLoad": "name",
		"directories": 
		[
			"Country"
		],
		"allMacroFileName": "Items"
	}
]
```

Using this conf file the file generates will be a macro file using the "name" property of the current feature. All the special charachter are deleted and replaced by '_'. Each macro name will start with an uppercase. 

To persist the name of all the macro, you can add the following item in the conf file:
```
	"allMacroFileName": "Items"
```

 At the prefix root a file name called "Items.mc2" will be generated. This file contains a mc2 macro which pushes on the stack a list that gives all the mc2 macro generated by this script.

