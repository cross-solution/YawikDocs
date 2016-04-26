.. index:: Organizations

Organizations
-------------

.. raw:: html

    <div style="float:right; width: 50%">
    <img src="https://www.transifex.com/projects/p/yawik/resource/organizations/chart/image_png"/>
    <br/>translation state of Core module.
    </div>

The organizations module adds a storage for organizations. If this module is enabled, a user can create an organization.
He can invite emploees via email to his organization. Employees can have the following roles

+--------------------+--------------------------------------------------------------+
| Role               | Description                                                  |
+====================+==============================================================+
| organization admin | Owner of an organization                                     |
+--------------------+--------------------------------------------------------------+
| recruiter          | Default Role of an employee                                  |
+--------------------+--------------------------------------------------------------+
| department manager | Department managers can accept or reject applications        |
+--------------------+--------------------------------------------------------------+
| manager            | currently unused                                             |
+--------------------+--------------------------------------------------------------+

In addition the following permissions can be set

+--------------------+---------------------------------------------------------------------------------+
| Permissions        | Description                                                                     |
+====================+=================================================================================+
| create jobs        | User can create job postings                                                    |
+--------------------+---------------------------------------------------------------------------------+
| edit jobs          | User can view and edit job postings                                             |
+--------------------+---------------------------------------------------------------------------------+
| view jobs          | User can view job postings                                                      |
+--------------------+---------------------------------------------------------------------------------+
| edit applications  | User can update applications. Eg. rate, invite, reject, etc                     |
+--------------------+---------------------------------------------------------------------------------+
| view applications  | User can view the application including attachments etc.                        |
+--------------------+---------------------------------------------------------------------------------+



Applicants refer to Organization Names in their work history. Job Postings require an Organization Name. Either
the name of the hiring Organization or the name of an agency. A Recruiter has to assign himself to an Organization.

Organization Names are just Names. They are public. Organization Names are assigned to various ratings. If an
Organization Name is used as an hiring Organization for a job posting, or if a recruiter is using an Organization
name for it's own company, the ranking is modified.

An Organization entity itself only contains a reference to an organization Name.


