#Authorisation

Content protection rules define which users, user groups and EGA’s are authorised to access
media files. The content protection rules can be set using the management application and the
EGA. An EGA can only set content protection rules for the media files stored in MediaMosa by
that EGA.

The rights can are assigned at asset level or on mediafile level. One of the options this offers is to provide
public access to a number of low-quality videos in an asset, providing access to a high-quality
version for a select group of users. Authorisation check takes place when the user requests a view on the mediafile.

When a media file is uploaded, it is not automatically protected: all users can view the file. If one
content protection rule is defined, the status changes to fully protected, except for the protection
rules as defined.

Content protection rules can be used to set the authorisation check for playback to:
* Domain
  An Internet domain name, such as: only give access to surfnet.nl. All subdomains (such as
  flex.surfnet.nl) would also have access.
* Realm
  Such as jan@xs4all.nl, or @surfnet.nl. In the first case, the realm must be an exact match
  for the party requesting the media file. The second case is more flexible: it gives access to
  all users that match *@surfnet.nl, as well as any subdomains (such as piet@surfnet.nl,
  jan@flex.surfnet.nl, joris@flex1.z33.surfnet.nl).
* Users 
  These are MediaMosa users. The user_id field is checked when playback is requested.
* Groups
  These are groups of MediaMosa users. The group_id field is checked when playback is
  requested.
* EGA’s
  This is a special variation on play rights. It is possible to assign play rights for the media file
  to other EGA’s that are linked to MediaMosa. To make this possible, the other EGA has to
  know the application ID. The media file will then be available to the public in that EGA,
  unless realm or domain rights have been set. If realm or domain rights have been defined,
  the other EGA also has to match those rights in order to view the media file. User and group
  rights for other EGA’s are ignored, since users and groups are unique to each EGA. A user
  or group from a different EGA can never own or have rights to a media file.

