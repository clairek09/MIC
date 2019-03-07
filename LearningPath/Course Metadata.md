# Advanced Settings                                                                         
---      
#### Advanced Module List	
###### It indicates what advanced modules used in your course
###### Put the modules's name (with quotation marks) in square brackets, and separates each using comma. 
```
advanced_modules:[
	"lti_consumer",
	"library_content"
]
```
---
#### Certificate Name (Long)	
###### Use this setting only when generating PDF certificates. Between quotation marks, enter the long name of the type of certificate that students receive when they complete the course. For instance, "Certificate of Achievement".
###### the $CourseTitle$ is a placeholder of Course Title, code will use the real course title to replace it

```
cert_name_long:"$CourseTitle$ Certificate"
```

---
#### Certificate Name (Short)	
###### Use this setting only when generating PDF certificates. Between quotation marks, enter the short name of the type of certificate that students receive when they complete the course. For instance, "Certificate".
###### the $CourseTitle$ is a placeholder of Course Title, code will use the real course title to replace it 
```
cert_name_short:"$CourseTitle$ Certificate"
```
---
#### Certificate Web/HTML View Enabled	
###### It indicates if Web/HTML views are enabled for the course or not
###### The allowed values is: true or false
```
cert_html_view_enabled:true
```
---
#### Certificates Display Behavior	
###### Use 'end', 'early_with_info', or 'early_no_info'. After certificate generation, students who passed see a link to their certificates on the dashboard and students who did not pass see information about the grading configuration. The default is end, which displays this certificate information to all students after the course end date. To display this certificate information to all students as soon as certificates are generated, enter early_with_info. To display only the links to passing students as soon as certificates are generated, enter early_no_info.
```
certificates_display_behavior:"early_with_info"
```
---
#### Course About Page Image	
###### It indicates what image will be used as the course about page image,
```
course_image:"images_course_image.jpg"
```
---
#### Course Display Name	
###### It indicates what name will be used as the name in the course list
###### the $CourseTitle$ is a placeholder of Course Title, code will use the real course title to replace it
```
display_name:"Dynamics: Power Platform integrations"
```
---
#### Course Number Display String	
###### Enter the course number that you want to appear in the course. 
```
display_coursenumber:""
```
---
#### Course Visibility In Catalog
###### Defines the access permissions for showing the course in the course catalog. This can be set to one of three values: 'both' (show in catalog and allow access to about page), 'about' (only allow access to about page), 'none' (do not show in catalog and do not allow access to an about page).
```
catalog_visibility:"both"
```

---
#### LTI Passports	
###### Enter the passports for course LTI tools in the following format: "id:client_key:client_secret".
###### Put the passport name (with quotation marks) in square brackets, and separates each using comma. 
```
lti_passports:[
    
] 
```
---
# Grading Setting
#### Overall Grade Range	
```
GRADE_CUTOFFS: {
		"Pass":0.70
    }
```
---
#### GRADER
```
GRADER: [
        {
            "drop_count": 0, 
            "min_count": 3, 
            "short_label": "KC", 
            "type": "Knowledge Check", 
            "weight": 0.6
        }, 
        {
            "drop_count": 0, 
            "min_count": 1, 
            "short_label": "Final", 
            "type": "Final Exam", 
            "weight": 0.4
        }
    ]
```

# Schedule And Details Settings

#### Course Pacing	
###### It indicates if enable Self-Paced
###### allowed Value: true or false
###### if assigns to 'false', the platform use Instructor-Paced mode. otherwise (assigns to 'true'), the platform use Self-paced mode.
###### Instructor-paced courses progress at the pace that the course author sets. You can configure release dates for course content and due dates for assignments.
###### Self-paced courses do not have release dates for course content or due dates for assignments. Learners can complete course material at any time before the course end date.

```
self_paced:true
```