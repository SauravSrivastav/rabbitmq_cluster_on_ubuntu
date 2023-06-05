Create a document that explains a piece of code to someone who has little to no technical background. Use clear and concise language, along with code examples, to make the content easy to follow. Be sure to include any necessary background information and avoid using technical jargon.

The code is: Here are the detailed step-by-step instructions related to clustering to set up a RabbitMQ cluster on three machines running Ubuntu 20.04 for production use from scratch in order:

**On each machine (Machine 1, Machine 2, and Machine 3):**

1. Edit the `/etc/hosts` file to add the hostnames and IP addresses of all machines:
```
sudo vi /etc/hosts
```
Add the following lines:
```
10.138.16.4 npprdw-rmq-node1
10.138.16.5 npprdw-rmq-node2
10.138.16.6 npprdw-rmq-node3
```
Save the file and exit the text editor.

This step ensures that each machine can resolve the hostnames of the other machines in the cluster.

**On Machine 1:**

2. Copy the `.erlang.cookie` file to Machine 2:
```
sudo scp /var/lib/rabbitmq/.erlang.cookie operatorrmq@10.138.16.5:/var/lib/rabbitmq/
```

The `.erlang.cookie` file is used by RabbitMQ for authentication between nodes in a cluster.

3. Copy the `.erlang.cookie` file to Machine 3:
```
sudo scp /var/lib/rabbitmq/.erlang.cookie operatorrmq@10.138.16.6:/var/lib/rabbitmq/
```

This step ensures that all machines in the cluster have the same cookie file.

**On Machine 2:**

4. Stop the RabbitMQ app:
```
sudo rabbitmqctl stop_app
```

5. Join the cluster with Machine 1:
```
sudo rabbitmqctl join_cluster rabbit@npprdw-rmq-node1
```

In this step, `rabbit` is the username of the RabbitMQ user on Machine 1 that Machine 2 is joining the cluster with. This username is automatically created by RabbitMQ and should not be changed.

6. Start the RabbitMQ app:
```
sudo rabbitmqctl start_app
```

This step joins Machine 2 to the cluster with Machine 1 as the disc node.

**On Machine 3:**

7. Stop the RabbitMQ app:
```
sudo rabbitmqctl stop_app
```

8. Join the cluster with Machine 1:
```
sudo rabbitmqctl join_cluster rabbit@npprdw-rmq-node1
```

In this step, `rabbit` is the username of the RabbitMQ user on Machine 1 that Machine 3 is joining the cluster with.

9. Start the RabbitMQ app:
```
sudo rabbitmqctl start_app
```

This step joins Machine 3 to the cluster with Machine 1 as the disc node.

**On Machine 1:**

10. Verify the cluster status:
```
sudo rabbitmqctl cluster_status
```

This command displays information about the current cluster status, including the nodes in the cluster and their running status.

That's it! These are the detailed step-by-step instructions related to clustering to set up a RabbitMQ cluster on three machines running Ubuntu 20.04 for production use from scratch in order.
