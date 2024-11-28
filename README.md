# AWS EC2 Instance Monitoring with CloudWatch Alarms and SNS Notifications

This project demonstrates how to monitor an AWS EC2 instance using **Amazon CloudWatch** alarms and notify administrators via **Amazon SNS** when an instance fails health checks or has insufficient data.

---

## Features
- Create and configure an EC2 instance.
- Set up CloudWatch alarms to monitor instance health using **StatusCheckFailed_Instance** metrics.
- Use **SNS (Simple Notification Service)** to send email alerts when alarms are triggered.
- Treat missing data as a threshold breach for better monitoring.

---

## Steps to Reproduce

### 1. **Launch an EC2 Instance**
1. Go to the AWS Management Console.
2. Navigate to **EC2 > Instances** and launch a new instance:
   - Select an AMI (e.g., Amazon Linux 2).
   - Choose an instance type (e.g., `t2.micro`).
   - Configure instance details and security group.
   - Launch the instance with a key pair.

---

### 2. **Create an SNS Topic for Notifications**
1. Navigate to **SNS > Topics** and click **Create Topic**.
2. Choose a topic type as **Standard** and provide a name, e.g., `ec2-web-status`.
3. Click **Create Topic**.
4. Under the topic, click **Create Subscription**:
   - **Protocol**: Email.
   - **Endpoint**: Enter your email address.
   - Confirm the subscription from your email inbox.

---

### 3. **Set Up a CloudWatch Alarm**
1. Navigate to **CloudWatch > Alarms** and click **Create Alarm**.
2. Select the **Metric**:
   - Click **Browse > EC2 > Per-Instance Metrics**.
   - Select your instance and choose **StatusCheckFailed_Instance**.
3. Configure the alarm:
   - **Name**: `web-status-alarm`.
   - **Threshold type**: Static.
   - **Condition**: Set it to trigger when metric value is **>= 1** for 1 data point.
   - **Treat Missing Data**: Select **Treat missing data as bad (breaching threshold)**.
4. Set **Alarm Actions**:
   - Add the SNS topic created earlier for **Alarm State** and **Insufficient Data State**.
5. Click **Create Alarm**.

---

### 4. **Test the Setup**
1. Simulate an alarm state:
   - Stop the EC2 instance to trigger the **StatusCheckFailed_Instance** alarm.
   - Confirm that an email notification is sent to your subscribed email address.
2. Restart the EC2 instance to verify the alarm returns to a healthy state.

---

## Project Structure
No specific code is required for this project. You can include screenshots of your AWS configurations:
- EC2 instance settings.
- SNS topic and subscription.
- CloudWatch alarm configurations.

---

## AWS Services Used
1. **Amazon EC2**: Virtual server hosting the monitored application.
2. **Amazon CloudWatch**: Monitoring and alarming for EC2 instance health.
3. **Amazon SNS**: Sending notifications to subscribed endpoints.

---

## Prerequisites
- AWS account with access to EC2, CloudWatch, and SNS services.
- Basic understanding of AWS monitoring and alerting.

---

## Future Improvements
- Integrate Lambda for automated responses when alarms are triggered.
- Monitor additional metrics like CPUUtilization or DiskReadOps.
- Use a custom health check script to complement **StatusCheckFailed_Instance**.

Please refer the Screenshots folder for execution
