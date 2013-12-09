**************************
Developer documents HOWTO
**************************
Before implementing you new functionality, everything has to be detailed in conception and technical documents:

1) Add your document in the appropriate page(s): 
* ((Spec_developers|Specifications))
* ((Developers_database|Database))
* ((Developers_rinor_rest|RINOR/REST))
* ((Developers_ui|UI))

2) Add and update the status regularly:
* 'draft' : The document is being created
* 'review' : The document is being reviewed, commented, corrected
* 'final' : The document is ready for application/implementation
* 'implemented 0.2.0' : The specification have been implemented on release x.y.z

2b) (Optional) A percentage bar can be added for more visual effect
{GAUGE(value=>50, max=>100, label=>''status'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
* 0% -> 30% : draft status
* 40% : review status
* 50% : final status
* 60% -> 90% : implementation
* 100% : fully implemented and tested
 
3) Add a status table at the top of each document.
||__Created:__|05/08/2011|(Date for when the document was created)
__Creator:__|Ferllings|(Initial creator of the document)
__Reviewers:__|Mirelsol, fritz_smh, Sp4rKy|(People who has reviewed/corrected/commented the document)
__Status:__|{GAUGE(value=>50, max=>100, label=>''final'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}|(current status, with an optional graph)
__Target:__|0.2.0
__References:__||Link to related Specs, Models, ...||