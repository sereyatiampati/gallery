# DevOps project
Building a jenkins pipeline that:
-  Facilitate deployment to Render with MongoDB, we'll be using [MongoDB Atlas](https://www.mongodb.com/atlas/database) a cloud-hosted MongoDB service. 
-  Pipeline triggers automatically whenever you push a new change to this repository. 
-  Pipeline executes the tests and should send an email if the tests fails. 
-  Slack integration and on a successful deploy, a slack message is sent on that channel.
-  The message includes the build ID, as well as the link to Render where the site is deployed. 