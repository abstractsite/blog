---
title: Super Generic Folder Layout (SGFL)
author: Marcus
layout: post
permalink: /super-generic-folder-layout-sgfl/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/08/super-generic-folder-layout-sgfl.html
categories:
  - Pipeline
---
Had a vision yesterday evening. A vision about how file handling could get more generic and less hard-coded.

## Solution

Previously, I&#8217;ve been thinking that each type of entity, like an asset or a sequence, could only have one type of child &#8211; assets have variants and sequences shots &#8211; so that there would be some structure in how the users worked.

<div>
  <img border="0" height="107px;" src="https://lh6.googleusercontent.com/0Iwp_jtmycjltVxV1z6WD_0WBF4kCIzPYcHDVBi4a_IEI1yYmLyv4EW8Ga4BdaYz6TcPEpnrZJlViztPOMFNeFdz7l7dkXjCVHTgT5ZefBMbvo-Z23dkeu-Q" width="277px;" />
</div>

<div>
  This is very constrained however and will not apply to how <u>everyone</u> works and might be rejected by those who don&#8217;t.</p> <div>
    <img border="0" height="85px;" src="https://lh3.googleusercontent.com/IuoLbx5ObUcklIgP_Wg0huLYa25qvypsl6XBQvDOfso4pQXk44F_bInaEqUIkqFCvFfjbiN0L8pQ75VwKSAqBoBTHCuKlbbccu-MF6TA6-GkhJ4A0t2poZ6HeA" width="116px;" />
  </div>
  
  <div>
  </div>
  
  <p>
    I&#8217;m thinking of generalising file management enough so that it basically acts like other file management app -Explorer on Windows versus Finder on OSX &#8211; where you can create any folder under any entity &#8211; like a shot under a job directly, skipping the sequence-parent. Or any random folder wherever.
  </p>
  
  <p>
    <span></span> <div>
      <img border="0" height="190" src="https://lh4.googleusercontent.com/zSu9enBNTQCQJa2foYUQUg_aj4PQGEEck-UShk6gGHctgKKiDW4smkySzDKFotACyTFGUte0Bn77E1j_mzv-L4E9AX84LXodrh7GhrFtZSlMsBMrV_sETjwe_A" width="200" />
    </div>
    
    <h3>
    </h3>
    
    <h3>
      Where&#8217;s the structure then?
    </h3>
    
    <div>
    </div>
    
    <h4>
      <b>Presets</b>
    </h4>
    
    <p>
      Once the user has created a project shell, like 1 sequence and 1 shot, they have essentially specified how they&#8217;ve chosen to structure their work.
    </p>
    
    <p>
      We could store that in a preset. So that for their next similar job, they could hit &#8220;Add by preset&#8221; which makes an empty shell identical to the one they saved.
    </p>
    
    <h4>
      <b>Templates</b> 
    </h4>
    
    <p>
      To expand on the pre-built types, like shot, asset or sequence, by letting users enter any type as the name, setting properties on their new type, and then saving it as a new type.
    </p>
    
    <p>
      Next time, they could enter that type and it would use their previous template.
    </p>
    
    <h1>
      Bottom Line
    </h1>
    
    <p>
      Making <b>Dashboard </b>more into the explorer enforces the one benefit of using the Dashboard over the explorer &#8211; Name conventions and placing of files and folders. That&#8217;s what they get and that&#8217;s what the Dashboard is supposed to take care of.
    </p>
    
    <h3>
      Benefit
    </h3>
    
    <p>
      More generic means more flexible. Advanced users will like it more and our development would get drastically simplified.
    </p>
    
    <h3>
      Disadvantage
    </h3>
    
    <p>
      More generic means less rigidity which may be counter-productive for new users who may need more hand-holding. But, this is where <b>presets</b> and <b>templates</b> would step in.</div>