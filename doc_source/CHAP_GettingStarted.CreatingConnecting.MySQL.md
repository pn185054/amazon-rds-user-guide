# Creating a MySQL DB instance and connecting to a database on a MySQL DB instance<a name="CHAP_GettingStarted.CreatingConnecting.MySQL"></a>

The easiest way to create a DB instance is to use the AWS Management Console\. After you have created the DB instance, you can use standard MySQL utilities such as MySQL Workbench to connect to a database on the DB instance\.

**Important**  
Before you can create or connect to a DB instance, make sure to complete the tasks in [Setting up for Amazon RDS](CHAP_SettingUp.md)\.

**Topics**
+ [Creating a MySQL DB instance](#CHAP_GettingStarted.Creating.MySQL)
+ [Connecting to a database on a DB instance running the MySQL database engine](#CHAP_GettingStarted.Connecting.MySQL)
+ [Deleting a DB instance](#CHAP_GettingStarted.Deleting.MySQL)

## Creating a MySQL DB instance<a name="CHAP_GettingStarted.Creating.MySQL"></a>

The basic building block of Amazon RDS is the DB instance\. This environment is where you run your MySQL databases\.

You can use **Easy create** to create a DB instance running MySQL with the AWS Management Console\. With **Easy create**, you specify only the DB engine type, DB instance size, and DB instance identifier\. **Easy create** uses the default settings for the other configuration options\. When you use **Standard create** instead of **Easy create**, you specify more configuration options when you create a database, including ones for availability, security, backups, and maintenance\.

In this example, you use **Easy create** to create a DB instance running the MySQL database engine with a db\.t2\.micro DB instance class\.

**Note**  
For information about creating DB instances with **Standard create**, see [Creating an Amazon RDS DB instance](USER_CreateDBInstance.md)\.

**To create a MySQL DB instance with Easy create**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the upper\-right corner of the Amazon RDS console, choose the AWS Region in which you want to create the DB instance\. 

1. In the navigation pane, choose **Databases**\.

1. Choose **Create database** and make sure that **Easy create** is chosen\.   
![\[Easy create option\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/easy-create-option.png)

1. In **Configuration**, choose **MySQL**\.

1. For **DB instance size**, choose **Free tier**\.

1. For **DB instance identifier**, enter a name for the DB instance, or leave the default name\.

1. For **Master username**, enter a name for the master user, or leave the default name\.

   The **Create database** page should look similar to the following image\.  
![\[Create database page\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/easy-create-mysql.png)

1. To use an automatically generated master password for the DB instance, make sure that the **Auto generate a password** box is selected\.

   To enter your master password, clear the **Auto generate a password** box, and then enter the same password in **Master password** and **Confirm password**\.

1. \(Optional\) Open **View default settings for Easy create**\.  
![\[Easy create default settings.\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/easy-create-view-default-mysql.png)

   You can examine the default settings used with **Easy create**\. The **Editable after database is created** column shows which options you can change after database creation\.
   + To change settings with **No** in that column, use **Standard create**\. 
   + To change settings with **Yes** in that column, either use **Standard create**, or modify the DB instance after it is created to change the settings\.

   The following are important considerations for changing the default settings:
   + In some cases, you might want your DB instance to use a specific virtual private cloud \(VPC\) based on the Amazon VPC service\. Or you might require a specific subnet group or security group\. If so, use **Standard create** to specify these resources\. You might have created these resources when you set up for Amazon RDS\. For more information, see [Provide access to your DB instance in your VPC by creating a security group](CHAP_SettingUp.md#CHAP_SettingUp.SecurityGroup)\.
   + If you want to be able to access the DB instance from a client outside of its VPC, use **Standard create** to set **Public access** to **Yes**\.

     If the DB instance should be private, leave **Public access** set to **No**\.

1. Choose **Create database**\.

   If you chose to use an automatically generated password, the **View credential details** button appears on the **Databases** page\.

   To view the master user name and password for the DB instance, choose **View credential details**\.  
![\[Master user credentials after automatic password generation.\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/easy-create-credentials.png)

   You can use the user name and password that appears to connect to the DB instance as the master user\.
**Important**  
You can't view the master user password again\. If you don't record it, you might have to change it\.   
If you need to change the master user password after the DB instance is available, you can modify the DB instance to do so\. For more information about modifying a DB instance, see [Modifying an Amazon RDS DB instance](Overview.DBInstance.Modifying.md)\.

1. In the **Databases** list, choose the name of the new MySQL DB instance\.

   On the RDS console, the details for new DB instance appear\. The DB instance has a status of **Creating** until the DB instance is ready to use\. When the state changes to **Available**, you can connect to the DB instance\. Depending on the DB instance class and the amount of storage, it can take up to 20 minutes before the new instance is available\.   
![\[Screenshot of the DB instance details.\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/MySQL-Launch06.png)

## Connecting to a database on a DB instance running the MySQL database engine<a name="CHAP_GettingStarted.Connecting.MySQL"></a>

After Amazon RDS provisions your DB instance, you can use any standard SQL client application to connect to a database on the DB instance\. In this example, you connect to a database on a MySQL DB instance using MySQL monitor commands\.

**To connect to a database on a DB instance using MySQL monitor**

1. Install a SQL client that you can use to connect to the DB instance\.

   You can connect to a MySQL DB instance by using tools like the mysql command line utility\. For more information on using the MySQL client, see[mysql \- the MySQL command\-line client](https://dev.mysql.com/doc/refman/8.0/en/mysql.html) in the MySQL documentation\. One GUI\-based application that you can use to connect is MySQL Workbench\. For more information, see the [Download MySQL Workbench](http://dev.mysql.com/downloads/workbench/) page\.

   For more information on using MySQL, see the [MySQL documentation](http://dev.mysql.com/doc/)\. For information about installing MySQL \(including the MySQL client\), see [Installing and upgrading MySQL](https://dev.mysql.com/doc/refman/8.0/en/installing.html)\.

   If your DB instance is publicly accessible, you can install the SQL client outside of your VPC\. If your DB instance is private, you typically install the SQL client on a resource inside your VPC, such as an Amazon EC2 instance\.

1. Make sure that your DB instance is associated with a security group that provides access to it\. For more information, see [Provide access to your DB instance in your VPC by creating a security group](CHAP_SettingUp.md#CHAP_SettingUp.SecurityGroup)\.

   If you didn't specify the appropriate security group when you created the DB instance, you can modify the DB instance to change its security group\. For more information, see [Modifying an Amazon RDS DB instance](Overview.DBInstance.Modifying.md)\.

1. Find the endpoint \(DNS name\) and port number for your DB instance\. 

   1. Open the RDS console and then choose **Databases** to display a list of your DB instances\. 

   1. Choose the MySQL DB instance name to display its details\. 

   1. On the **Connectivity & security** tab, copy the endpoint\. Also, note the port number\. You need both the endpoint and the port number to connect to the DB instance\.   
![\[Connect to a MySQL DB instance\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/MySQLConnect1.png)

1. Connect to the a database on a MySQL DB instance\. For example, enter the following command at a command prompt on a client computer to connect to a database on a MySQL DB instance using the MySQL client\. Substitute the DNS name for your DB instance for `<endpoint>`\. In addition, substitute the master user name that you used for `<mymasteruser>`, and provide the master password that you used when prompted for a password\.

   ```
   PROMPT> mysql -h <endpoint> -P 3306 -u <mymasteruser> -p
   ```

   After you enter the password for the user, you should see output similar to the following\.

   ```
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 350
   Server version: 5.6.40-log MySQL Community Server (GPL)
   
   Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
   
   mysql>
   ```

For more information about connecting to a MySQL DB instance, see [Connecting to a DB instance running the MySQL database engine](USER_ConnectToInstance.md)\. If you can't connect to your DB instance, see [Can't connect to Amazon RDS DB instance](CHAP_Troubleshooting.md#CHAP_Troubleshooting.Connecting)\.

## Deleting a DB instance<a name="CHAP_GettingStarted.Deleting.MySQL"></a>

After you have connected to the sample DB instance that you created, you should delete the DB instance so you are no longer charged for it\. 

**To delete a DB instance with no final DB snapshot**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**\.

1. Choose the DB instance that you want to delete\.

1. For **Actions**, choose **Delete**\.

1. For **Create final snapshot?**, choose **No**, and select the acknowledgment\. 

1. Choose **Delete**\. 