# spring-bosh

A simple demo to deploy and run the getting-started Spring Boot application using BOSH.

This assumes that the bosh lite director is up and running and the routes are configured already.

The director uuid needs to be updated in the manifest file. And a deployment needs to be created.

Once done, in order get this working, the binary blobstore needs to be additionally created:

blobs
├── gs-spring-boot
│   └── target
│       └── gs-spring-boot-0.1.0.jar -> .blobstore...
└── java
    └── jre-8u111-linux-x64.tar.gz -> .blobstore...

Once the blobs are created, they need to be uploaded.
Now comes the fun part:

$ bosh create release
$ bosh upload release
$ bosh -n deploy

And that's it.

There should be now 2 vms running:

+------------------------------------------------------+---------+-----+---------+-------------+
| VM                                                   | State   | AZ  | VM Type | IPs         |
+------------------------------------------------------+---------+-----+---------+-------------+
| spring-boot/0 (fc2e5f34-11c1-4473-8a69-9e8dc4ae399f) | running | n/a | default | 10.244.0.10 |
| spring-boot/1 (0cc12455-8554-408f-b2d5-a4759d5603d3) | running | n/a | default | 10.244.0.9  |
+------------------------------------------------------+---------+-----+---------+-------------+
