.. index:: Core; Imagesets

Image sets
----------

:Author: Mathias Gelhausen <gelhausen@cross-solution.de>

An image set in YAWIK are multiple different sized versions of one image.

Organizations uses an image set to store the organization logo as thumbnail, medium and large versions.

Each version of the image has its own key to identify, which can be any string - however there are two special
key names currently defined in ``\Core\Entity\ImageSetInterface``, THUMBNAIL and ORIGINAL, which refers to the
thumbnailed version and the original uploaded version of the image obviously.

Get/Set an image from/to the set
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You retrieve a version of the image, by calling the ``get`` method of the image set entity.

.. code-block:: php

     // get the thumbnail image entity
     $thumb = $imageSet->get(ImageSetInterface::THUMBNAIL);

     // set a version of the image
     $imageSet->set('medium', $image);

     // get a version of the image
     $image = $imageSet->get('medium');

     // get original image
     $image = $imageSet->get();




