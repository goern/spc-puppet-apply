# This is an SPC (super privileged container) for puppet apply.

It is distributed with an omv.yaml file for ease in setting up and testing an
example environment built by Oh-My-Vagrant. Nothing in this SPC *depends* on
Oh-My-Vagrant, but if you don't use the project then you obviously must provide
your own virtual machine test environment.

If you are using Oh-My-Vagrant, after a successful "vup", you should have a
docker image built:

```
# docker images | grep spc
spc-puppet-apply    latest              72f2dfbc4e07        7 minutes ago       314.5 MB
```

As a test application, this project supplies a test.pp example. You can copy it
to somewhere that is readable by your container, for example to: /var/tmp/

```
# mkdir /var/tmp/spc-puppet-apply/
# cp -a /vagrant/docker/spc-puppet-apply/test.pp /var/tmp/spc-puppet-apply/
```

Please note that if you are using Oh-My-Vagrant with the Atomic host, you will
instead find the example files in: /home/vagrant/sync/docker/spc-puppet-apply/

Finally, run the container and point to the container accessible .pp file that
you would like to "apply":

```
# docker run --rm -it --privileged -v /etc:/etc -v /var:/var -v /run:/run --net=host spc-puppet-apply /var/tmp/spc-puppet-apply/test.pp
Notice: Compiled catalog for omv1.example.com in environment production in 0.02 seconds
Notice: This is a puppet test!

Notice: /Stage[main]/Main/Notify[hello]/message: defined 'message' as 'This is a puppet test!
'
Notice: Finished catalog run in 0.06 seconds
```

Please note that running an SPC should be a lot simpler when using the atomic
command, as this SPC supports the atomic run label.

Happy hacking!
James
@purpleidea
