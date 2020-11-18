使用tensorboard查看linux服务器上的记录

先在linux服务器工程目录下执行：tensorboard --logdir=tf_log_path --host=0.0.0.0 --port 6006

然后在浏览器输入网址：http://172.16.2.119:6006