# ckanext-grouphierarchy - group hierarchy for CKAN

Provides a new field on the group edit form to select a parent
group. This new hierarchical arrangement of groups is displayed
using templates in this extension, instead of the usual list. An group
page also displays the section of the tree.
This version (0.2) of this extension also supports the group labeling on the dataset page and on the search page where the datasets are listed. Please note the labeling is only for the main group [id='main-categories'] including 9 sub-groups/children. 

Forms (hierachy_form plugin):
* /group/new
* /group/edit/{id}

Templates (hierarchy_display plugin):
* /group - now shows the group hierarchy instead of list
* /group/about/{id} - now also shows the relevant part of the hierarchy

Please note that the categories of groups are hard coded.
github.com/tum-gis/ckanext-grouphierarchy-sddi/blob/master/ckanext/grouphierarchy/templates/group/snippets/group_list.html


Snippets (used by hierarchy_display and ckanext-scheming):
* /scheming/form_snippets/group_hierarchy.html

You can use this extension with CKAN as it is, enabling both plugins. Or if you
use an extension to customise the form already with an IGroupForm, then you
will want to only use the hierarchy_display plugin, and copy bits of the
hierarchy_form into your own. If you have your own templates then you can use
the snippets (or logic functions) that this extension provides to display the
trees.

In order to make hierarchy works with ckanext-scheming you need to enable just
hierarchy_display and then use corresponding form_snippet in your org_schema.
For example, you may add next field:
```
{
    "field_name": "not_used",
    "label": "Parent group",
    "display_snippet": null,
    "form_snippet": "group_hierarchy.html",
    "validators": "ignore_missing"
}
```

## Compatibility

This extension has been tested with CKAN v2.8.0 or later. 

## Installation

Install the extension in your python environment
```
$ . /usr/lib/ckan/default/bin/activate
(pyenv) $ cd /usr/lib/ckan/default/src
(pyenv) $ pip install -e "git+https://tum-gis/ckanext-grouphierarchy-sddi.git#egg=ckanext-grouphierarchy-sddi"
```
Then change your CKAN ini file (e.g. development.ini or production.ini).  Note that display_group
should come before form_group
```
ckan.plugins = stats text_view recline_view ... display_group form_group
```

Important: This Extension only works if you have the parent groups "main-categories" ("Hauptkategorien") and "topics" ("Themen"). You will get an error if you do not use these groups.

## Copyright & Licence

This module is Crown Copyright 2013 and openly licensed with AGPLv3 - see LICENSE file.
