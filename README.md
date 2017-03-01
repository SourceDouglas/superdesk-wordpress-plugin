# What is the Wordpress Superdesk Publisher plugin?
The Superdesk Wordpress Publisher plugin enables content to be sent from an instance of Sourcefabric's Superdesk newsroom management system (www.superdesk.org) and the Wordpress instance it's installed on. Superdesk itself is open source (https://github.com/superdesk/superdesk).

# What does the Wordpress Superdesk Publisher plugin do?
When both Superdesk and the Wordpress Superdesk Publisher plugin are correctly configured, a Superdesk user publishes an item and it is automatically published in Wordpress. Users can still log in to Wordpress to administer the site.

# How does it work?
Superdesk supports the IPTC's industry standard ninjs (http://dev.iptc.org/ninjs), which standardizes the representation of news in JSON - a lightweight, easy-to-parse, data interchange format. The Superdesk Wordpress Publisher plugin will also enable multiple instances of Wordpress to receive content from a single instance of Superdesk; output channels are defined in Superdesk, so you could have multiple, or only one, or none at all (which wouldn't be that useful but still possible (wink)). This plugin should also work with other information sources that use ninjs.

We've created a table to map fields between Superdesk's ninjs implementation and Wordpress: https://wiki.sourcefabric.org/display/NR/Ninjs+to+WP+data+structure+mapping

On the Superdesk side, there are publishing providers which are the ones in charge of actually delivering the content in the configured format and delivery mechanism; this is done on a publishing channel basis in Superdesk.

Stories are checked in Superdesk as published, then the publishing providers take over to distribute the content.

The Superdesk Wordpress Publisher plugin currently uses Superdesk's HTTP PUSH to receive content in ninjs. When an article is published in Superdesk, an HTTP PUSH is sent to this address:

http://path-to-your-wordpress-instance/wp-content/plugins/superdesk-wordpress-plugin-master/autoload.php

The Superdesk ninjs file looks like this:

```json
{
  "priority": 6,
  "subject": [
    {
      "code": "03005000",
      "name": "flood"
    },
    {
      "code": "06003000",
      "name": "energy saving"
    }
  ],
  "description_html": "<p>This is a test of field updates. We will update the author and copyright fields in this test to make sure all fields are updated.</p>",
  "urgency": 3,
  "version": "3",
  "guid": "urn:newsml:localhost:2017-02-27T13:37:35.512526:aa1abad3-d634-4453-a449-d13a69e8ef4c",
  "description_text": "This is a test of field updates. We will update the author and copyright fields in this test to make sure all fields are updated.",
  "profile": "58468fca9cb59b004943c30b",
  "body_html": "<p style=\"margin-bottom: 15px; text-align: justify; color: rgb(0, 0, 0); font-family: &quot;Open Sans&quot;, Arial, sans-serif; font-size: 14px; background-color: rgb(255, 255, 255);\">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus at aliquam elit. Praesent at commodo mauris. Aliquam in enim et ipsum porta volutpat. Cras turpis nulla, suscipit sed metus vel, maximus dictum est. Duis vehicula ante non fringilla aliquam. Morbi pulvinar ex sed lectus blandit, vel pellentesque velit eleifend. Nunc non purus nunc.</p><p style=\"margin-bottom: 15px; text-align: justify; color: rgb(0, 0, 0); font-family: &quot;Open Sans&quot;, Arial, sans-serif; font-size: 14px; background-color: rgb(255, 255, 255);\">Ut lectus ligula, fringilla sed varius a, dictum eu dui. Mauris id tellus ut ipsum ullamcorper luctus. Maecenas ullamcorper ante nec neque commodo semper. Aenean aliquet nulla nisl. Ut arcu dolor, euismod vel urna eu, aliquam varius quam. Etiam lacinia posuere efficitur. In luctus maximus tortor in dignissim. Quisque imperdiet nunc enim, non aliquet lectus venenatis ullamcorper. Donec et diam eget augue porttitor consequat in id augue.</p><p style=\"margin-bottom: 15px; text-align: justify; color: rgb(0, 0, 0); font-family: &quot;Open Sans&quot;, Arial, sans-serif; font-size: 14px; background-color: rgb(255, 255, 255);\">Nam vitae nisl congue, iaculis ligula in, cursus nisi. Donec hendrerit lorem non sem consectetur euismod. Cras eu est porttitor, placerat est in, tristique tortor. Pellentesque tristique lorem et neque euismod imperdiet. In accumsan magna non ipsum euismod maximus non vitae tellus. Sed tristique lectus sit amet augue luctus condimentum. Suspendisse potenti. In blandit sodales augue quis luctus. In hac habitasse platea dictumst. Sed felis risus, blandit in turpis vel, vestibulum dapibus urna. Cras cursus porta est, id tempor ante vestibulum nec.</p><p style=\"margin-bottom: 15px; text-align: justify; color: rgb(0, 0, 0); font-family: &quot;Open Sans&quot;, Arial, sans-serif; font-size: 14px; background-color: rgb(255, 255, 255);\">Nulla vitae lorem eu leo cursus elementum vitae sit amet mauris. Phasellus a mauris volutpat diam malesuada pretium. Donec sed leo accumsan, elementum nulla eget, mattis felis. In et aliquet odio, vel molestie mi. Etiam semper nisi ac lorem egestas dictum. Proin luctus porta dui, faucibus pellentesque urna venenatis quis. Morbi mi risus, volutpat ut diam non, pulvinar laoreet odio. Vivamus pharetra feugiat vestibulum. Nulla pharetra id purus vel consequat. Sed aliquam maximus luctus. Fusce ultrices urna sed felis porttitor gravida. Nam posuere ex eu orci posuere, ac posuere augue accumsan. Proin rhoncus neque vel neque euismod, non feugiat odio lacinia. Curabitur porta sapien eget tortor egestas elementum vitae laoreet mi.</p>",
  "versioncreated": "2017-02-27T13:40:26+0000",
  "language": "en",
  "firstcreated": "2017-02-27T13:37:35+0000",
  "service": [
    {
      "code": "a",
      "name": "Australian General News"
    },
    {
      "code": "p",
      "name": "Federal Parliament"
    }
  ],
  "type": "text",
  "headline": "Testing field updates",
  "located": "Herat",
  "pubstatus": "usable",
  "place": [
    
  ],
  "slugline": "testing-field-update",
  "associations": {
    "featuremedia": {
      "place": [
        
      ],
      "renditions": {
        "thumbnail": {
          "poi": {
            "x": 80,
            "y": 60
          },
          "mimetype": "image/jpeg",
          "href": "https://superdesk-test.s3-eu-west-1.amazonaws.com/sd-wpp/20170227130236/8970158ec49f76e9ea5f4860ddf2a0d065c085bc77f5eb6a92d480bbf8701f2e.jpg",
          "media": "sd-wpp/20170227130236/8970158ec49f76e9ea5f4860ddf2a0d065c085bc77f5eb6a92d480bbf8701f2e.jpg",
          "width": 160,
          "height": 120
        },
        "original": {
          "poi": {
            "x": 1296,
            "y": 968
          },
          "mimetype": "image/jpeg",
          "href": "https://superdesk-test.s3-eu-west-1.amazonaws.com/sd-wpp/20170227130236/da3d83bbc3655d6262e73fd3c57be96e81c969644cf6c37fee0ed55c82cb1654.jpg",
          "media": "sd-wpp/20170227130236/da3d83bbc3655d6262e73fd3c57be96e81c969644cf6c37fee0ed55c82cb1654.jpg",
          "width": 2592,
          "height": 1936
        },
        "baseImage": {
          "poi": {
            "x": 700,
            "y": 522
          },
          "mimetype": "image/jpeg",
          "href": "https://superdesk-test.s3-eu-west-1.amazonaws.com/sd-wpp/20170227130236/497c7cc586729affa2d8717964ff967a44e6d0975c41e5a43df5b8476c7e5dbe.jpg",
          "media": "sd-wpp/20170227130236/497c7cc586729affa2d8717964ff967a44e6d0975c41e5a43df5b8476c7e5dbe.jpg",
          "width": 1400,
          "height": 1045
        },
        "16-9": {
          "poi": {
            "x": 1296,
            "y": 733
          },
          "mimetype": "image/jpeg",
          "href": "https://superdesk-test.s3-eu-west-1.amazonaws.com/sd-wpp/20170227130236/6d9320f8-a40f-4054-80f1-71671477834b.jpg",
          "media": "sd-wpp/20170227130236/6d9320f8-a40f-4054-80f1-71671477834b.jpg",
          "width": 1280,
          "height": 720
        },
        "4-3": {
          "poi": {
            "x": 1296,
            "y": 968
          },
          "mimetype": "image/jpeg",
          "href": "https://superdesk-test.s3-eu-west-1.amazonaws.com/sd-wpp/20170227130236/cdb48154-154a-4fcd-9f7c-f1b174b655db.jpg",
          "media": "sd-wpp/20170227130236/cdb48154-154a-4fcd-9f7c-f1b174b655db.jpg",
          "width": 798,
          "height": 600
        },
        "viewImage": {
          "poi": {
            "x": 320,
            "y": 239
          },
          "mimetype": "image/jpeg",
          "href": "https://superdesk-test.s3-eu-west-1.amazonaws.com/sd-wpp/20170227130236/d237b77b0a0cbaa647174b5ede87975d9532741907772081ae8399f2d6d61126.jpg",
          "media": "sd-wpp/20170227130236/d237b77b0a0cbaa647174b5ede87975d9532741907772081ae8399f2d6d61126.jpg",
          "width": 640,
          "height": 478
        }
      },
      "body_text": "Krumlov",
      "mimetype": "image/jpeg",
      "urgency": 3,
      "version": "2",
      "priority": 6,
      "copyrightholder": "Joe Bloggs",
      "usageterms": "indefinite-usage",
      "description_text": "Krumlov",
      "language": "en",
      "versioncreated": "2017-02-27T13:39:21+0000",
      "headline": "Krumlov",
      "service": [
        {
          "code": "a",
          "name": "Australian General News"
        }
      ],
      "copyrightnotice": "(c) 2017 Sourcefabric",
      "type": "picture",
      "firstcreated": "2017-02-27T13:39:17+0000",
      "located": "Herat",
      "pubstatus": "usable",
      "guid": "tag:localhost:2017:97e42b1c-74de-4821-9981-c581baa564c5",
      "byline": "Joe Bloggs"
    }
  },
  "byline": "By Douglas Arellanes"
}
```

# What's next?
We do not have a native Wordpress publishing provider in Superdesk, and there is no plan to write one in the current roadmap. We prefer to use ninjs as an standard interchange format.
