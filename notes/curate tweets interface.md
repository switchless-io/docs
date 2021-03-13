# Curate tweets interface

## curate_raw_tweets.ejs
```
<div class="ui five item menu">
  <a class="item <%if(classification=='curation_required'){%>active<%}%>" href='/curator/curate_raw_tweets/curation_required?<%if(track_id){%>track=<%=track_id%><%}%>'>Curation Required (<%=count.curation_required%>)</a>
  <a class="item <%if(classification=='educational'){%>active<%}%>" href='/curator/curate_raw_tweets/educational?<%if(track_id){%>track=<%=track_id%><%}%>'>Educational (<%=count.educational%>)</a>
  <a class="item <%if(classification=='neutral'){%>active<%}%>" href='/curator/curate_raw_tweets/neutral?<%if(track_id){%>track=<%=track_id%><%}%>'>Neutral (<%=count.neutral%>)</a>
  <a class="item <%if(classification=='spam'){%>active<%}%>" href='/curator/curate_raw_tweets/spam?<%if(track_id){%>track=<%=track_id%><%}%>'>Spam (<%=count.spam%>)</a>
  <a class="item <%if(classification=='curate_later'){%>active<%}%>" href='/curator/curate_raw_tweets/curate_later?<%if(track_id){%>track=<%=track_id%><%}%>'>Curate_later (<%=count.curate_later%>)</a>
</div>
<div class='ui container'>
  <!-- this contains the filter button -->
  <div class="ui labeled icon top left pointing dropdown button">
    <i class="filter icon"></i>
    <span class="text">
      <%if(!filter.type){%>
        Filter Tweets
      <%}else if(filter.type=='list'){%>
        <div class="ui red empty circular label"></div><%=filter.text%>
      <%}else if(filter.type=='track'){%>
        <div class="ui blue empty circular label"></div><%=filter.text%>
      <%}else if(filter.type=='influencer'){%>
        <div class="ui green empty circular label"></div><%=filter.text%>
      <%}%>
    </span>
    <div class="menu">
     
      <div class="header">
        <i class="tags icon"></i>
        Filter by Lists
      </div>
      <% _.each(lists,function(list){%>
        <a class="item" href='?list=<%=list.id%>'>
          <div class="ui red empty circular label"></div>
          <%=list.name%>
        </a>
      <%})%>
      <div class="divider"></div>
      <div class="header">
        <i class="calendar icon"></i>
        Filter by Track
      </div>
      <% _.each(tracks,function(track){%>
        <a class="item" href='?track=<%=track.id%>'>
          <div class="ui blue empty circular label"></div>
          <%=track.name%>
        </a>
      <%})%>
      <div class="divider"></div>
      <div class="header">
        <i class="calendar icon"></i>
        Filter by Influencers
      </div>
      <% _.each(influencers,function(influ){%>
        <a class="item" href='/curator/curate_raw_tweets/curation_required?influencer=<%=influ.username%>'>
          <div class="ui green empty circular label"></div>
          <%=influ.name%>
        </a>
      <%})%>
      
    </div>
  </div>
</div>
<div class='ui stackable grid'>
  <div class='ten wide column'>
    <% _.each(tweets,function(tweet){%>
      <%if(tweet.raw.user){%>
      <div class='ui stackable grid' id='tweet_<%=tweet.id%>'>
        <div class='three wide computer only column'>
        </div>
        <div class='eight wide column'>
          <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><%=tweet.raw.text%></p>&mdash; <%=tweet.raw.user.name%> (@<%=tweet.raw.user.screen_name%>) <a href="https://www.twitter.com/<%=tweet.raw.user.screen_name%>/status/<%=tweet.raw.id_str%>"></a></blockquote>
        </div>
        <div class='five wide column'>
          <%if(tweet.details){%>
          <b>type</b> : <%=tweet.details.type%><br>
          <b>urls_count</b> : <%=tweet.details.urls_count%><br>
          <b>own_content</b>? : <%=tweet.details.own_content%><br>
          <b>share_url</b> : <%=tweet.details.share_url%><br>
          <b>possible_topics</b> : <%=tweet.details.possible_topics%><br>
          
          <%if(tweet.details.item){%>
            <b>item.url</b> : <span id='item_url_<%=tweet.id%>'><%=tweet.details.item.url%></span><br>
            <b>item.name</b> : <span id='item_name_<%=tweet.id%>'><%=tweet.details.item.name%></span><br>
            <b>item.type</b> : <span id='item_type_<%=tweet.id%>'><%=tweet.details.item.type%></span><br>
          <%}%>
          <!-- <b>repeat_count</b> : <%=tweet.details.repeat_count%><br> -->
          <%}%>
          
          <div class='ui center aligned segment' id='action_<%=tweet.id%>'>
            <div ><b>Curate this tweet : </b></div>
            <div class="four ui small buttons">
              <button class="ui toggle button change_classification <%if(classification=='curation_required'){%>active<%}%>" data-new-classification='curation_required' data-id='<%=tweet.id%>'>CR</button>
              <button class="ui toggle button change_classification <%if(classification=='educational'){%>active<%}%>" data-new-classification='educational' data-id='<%=tweet.id%>'>Edu</button>
              <button class="ui toggle button change_classification <%if(classification=='neutral'){%>active<%}%>" data-new-classification='neutral' data-id='<%=tweet.id%>'>Ntrl</button>
              <button class="ui toggle button change_classification <%if(classification=='spam'){%>active<%}%>" data-new-classification='spam' data-id='<%=tweet.id%>'>Spam</button>
              <!-- <button class="ui toggle button">Support</button> -->
            </div>

            <%if(classification=='wall_of_love'){%>
              <a class='change_classification' data-new-classification='curation_required' data-id='<%=tweet.id%>' href="#">Mark as curation required</a><br/>
              <a class='change_classification' data-new-classification='discarded' data-id='<%=tweet.id%>' href="#">Discard</a>
            <%}%>
            <%if(classification=='discarded'){%>
              <a class='change_classification' data-new-classification='curation_required' data-id='<%=tweet.id%>' href="#">Mark as curation required</a><br/>
              <a class='change_classification' data-new-classification='wall_of_love' data-id='<%=tweet.id%>' href="#">Add to wall of love</a><br/>
            <%}%>
            <%if(classification=='educational'){%>
            <div class="ui divider"></div>
              <a class="ui button" href="/curator/item/create_with_review?tweet_id=<%=tweet.id%>">Convert to review</a>
            <%}%>
          </div>
        </div>
        
      </div>
      <div class='ui divider'></div>
      <%}%>
    <%});%>
    <!-- <button class='ui fluid button' onClick="window.location.reload()">Reload</button> -->
    <div class="ui two item menu">
        
        
      <a class="pagination <%if(!tweets_from){%> disabled <%}%> item" data-page='<%=pg.pagination.page-1%>' onclick="goBack()">
      <i class="left chevron icon"></i>
      Back
      </a>

      

      <a class="pagination <% if(pg.pagination.page==Math.ceil(pg.pagination.total_pages)){%> disabled<%}%> item" data-page='<%=Number(pg.pagination.page)+1%>' href="?<%if(track_id){%>track=<%=track_id%>&<%}%>tweets_from=<%=last_tweet%>">
        Next
        <i class="right chevron icon"></i>
      </a>
      
      
    </div>
  </div>
  <div class='six wide column'>
  </div>
</div>


<div class="ui small modal input_proper_item_url">
  <i class="close icon"></i>
  <div class="header">
    Item url does not seem right
  </div>
  <div class="content">
    <div class="description">
      <!-- <div class="ui header">We've auto-chosen a profile image for you.</div> -->
      <h5>Item url : <a href="" id='modal_item_url'></a></h5>
      <h5>Raw Tweet id : <span id='modal_raw_tweet_id'></span></h5>
      <p>Item that you are saying is educational is a link to a tweet. You are probably referring to something else in the tweet that is educational. I am not able to extract it. Please enter the actual url of the item in the tweet, that you think is educational.</p>
      <div class="ui fluid input">
        <input id='actual_item_url' type="text" placeholder="Enter actual item url">
      </div>
    </div>
    <div class='when_loading' style="display: none;">
      <h5>Extracting details from new url </h5>
    </div>
    
  </div>
  <div class="actions">
    <button class="ui red deny button" >
      Cancel
    </button>
    <button class="ui blue approve button">
      Submit
    </button>
  </div>
</div>


<div class="ui small modal confirm_item_url">
  <i class="close icon"></i>
  <div class="header">
    Fetching details of the url that you submitted
  </div>
  <div class="content">
    <div class="description">
      <!-- <div class="ui header">We've auto-chosen a profile image for you.</div> -->
      <h5>Item url : <a href="" id='modal_item_url_submitted'></a></h5>
      <div class="ui active centered inline loader"></div>
      <b>Item Name:</b> <span id='submitted_item_url_name'></span><br/>
      <b>Item Type:</b> <span id='submitted_item_url_type'></span><br/>
      <b>Item Author:</b> <span id='submitted_item_url_author'></span><br/>
      <b>Item Image:</b> <span id='submitted_item_url_image'></span><br/>
      
    </div>
  </div>
  <div class='when_loading' style="display: none;">
      <p>The item details in the raw_tweet is getting updated. It will also get marked as educational</p>
    </div>
  <div class="actions">
    <button class="ui red deny button" >
      Cancel
    </button>
    <button class="ui blue approve button">
      Update item details
    </button>
  </div>
</div>
<script type="text/javascript">

  var removeParams=function(keys, sourceURL) {
    //removes all params in keys from sourceURL
    //
    //Declaring variables
        var result = sourceURL.split("?")[0];//
        var param;
        var params_arr = []
        var queryString = (sourceURL.indexOf("?") !== -1) ? sourceURL.split("?")[1] : "";


        if (queryString !== "") {
            params_arr = queryString.split("&");
            for (var i = params_arr.length - 1; i >= 0; i -= 1) {
                param = params_arr[i].split("=")[0];
                if (keys.indexOf(param)>-1) {
                    params_arr.splice(i, 1);
                }
            }
            if(params_arr.length>0)
                result = result + "?" + params_arr.join("&");
        }
      return result;
  }

  $(document).ready(function(){
    var raw_tweet={
      //id
      //details
    }
    $('.ui.modal').modal({
      allowMultiple: false
    });
    $('.modal.input_proper_item_url').modal({
      closable  : false,
      onDeny    : function(){
        return true;
      },
      onApprove : function() {
        $('.modal.input_proper_item_url .approve').addClass('loading');
        $('.modal.input_proper_item_url .deny').addClass('disabled');
        $('.modal.input_proper_item_url .description').hide();
        $('.modal.input_proper_item_url .when_loading').show();
        var data={
          url:$('#actual_item_url').val()
        }
        $.post("/api/c/get_item_details",data, function(responseText, classification,result){
          // alert("Data: " + data + "\nResult: " + result);
          raw_tweet.details={
            item:result.responseJSON.item
          }
          if(classification=='success'){

            // $('#tweet_'+tweet).fadeOut();
            // button.parent().children().removeClass('active');
            // $('#action_'+tweet).removeClass('loading');
            // button.addClass('active');
            $('.modal.input_proper_item_url .approve').removeClass('loading');
            $('.modal.input_proper_item_url .deny').removeClass('disabled');
            $('.modal.input_proper_item_url .description').show();
            $('.modal.input_proper_item_url .when_loading').hide();

            $('#submitted_item_url_name').html(result.responseJSON.item.name);
            $('#submitted_item_url_type').html(result.responseJSON.item.type);
            $('#modal_item_url_submitted').html(result.responseJSON.item.url);
            $('#submitted_item_url_author').html(result.responseJSON.item.details.author);
            $('#submitted_item_url_image').html(result.responseJSON.item.details.image);
            $('.modal.confirm_item_url').modal('show');
          } else alert('something went wrong');
        });
        return false;
      }
    })
    $('.modal.confirm_item_url').modal({
      closable  : false,
      onDeny    : function(){
        return true;
      },
      onApprove : function() {
        $('.modal.confirm_item_url .approve').addClass('loading');
        $('.modal.confirm_item_url .deny').addClass('disabled');
        var data={
          raw_tweet_id:raw_tweet.id,
          details:raw_tweet.details
        }
        console.log(data);
        $.post("/api/c/updateRawTweetDetails",data, function(responseText, classification,result){
          // alert("Data: " + data + "\nResult: " + result);
          if(classification=='success'){

            $('#item_url_'+raw_tweet.id).text(raw_tweet.details.item.url);
            $('#item_name_'+raw_tweet.id).text(raw_tweet.details.item.name);
            $('#item_type_'+raw_tweet.id).text(raw_tweet.details.item.type);
            $('.modal.confirm_item_url .approve').removeClass('loading');
            $('.modal.confirm_item_url .deny').removeClass('disabled');
            $('.modal.confirm_item_url .description').show();
            $('.modal.confirm_item_url .when_loading').hide();

            $('.modal.confirm_item_url').modal('hide');
          } else alert('something went wrong');
        });
        return false;
      }
    })
    // $('.modal.confirm_item_url').modal('attach events', '.modal.input_proper_item_url .approve')
    //pagination
    // $('a.pagination').click(function(){
    //   var page=$(this).attr('data-page');
    //   console.log('page= '+page);
    //   var current_url=window.location.href;
    //   if(current_url.indexOf("?")!=-1)//if ? exists
    //     window.location=removeParams(['page'],window.location.href)+'&page='+page;
    //   else
    //     window.location=removeParams(['page'],window.location.href)+'?page='+page;


    // });

    /**
     * Change classification of the tweet to wall_of_love
     */
    $('.change_classification').click(function(){
      var tweet=$(this).attr('data-id');
      var classification=$(this).attr('data-new-classification');
      var item_url=$('#item_url_'+tweet).text();
      var button=$(this);
      if(item_url.indexOf('twitter.com/i/web/status/')>0 && classification=='educational'){
        $('#modal_item_url').attr('href',item_url);
        $('#modal_item_url').html(item_url);
        $('#modal_raw_tweet_id').html(tweet);
        raw_tweet.id=tweet;
        raw_tweet.this=$(this);
        $('.input_proper_item_url').modal('show');
      }
      else{
        var data={
          tweet:tweet,
          classification:classification,
        };
        button.parent().children().removeClass('active');
        $('#action_'+tweet).removeClass('loading');
        button.addClass('active');
        $('#action_'+tweet).addClass('loading');
        $.post("/curator/change_classification_of_one_tweet",data, function(responseText, classification,result){
          if(classification=='success'){
            button.parent().children().removeClass('active');
            $('#action_'+tweet).removeClass('loading');
            button.addClass('active');
          }else alert('something went wrong');
        });
      }
    });
  });
</script>


<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


<script type="text/javascript">
  $(document).ready(function(){
    $('.ui.dropdown').dropdown();
  })


</script>


<script>
  function goBack() {
      window.history.back()
  }
</script>

```

## Controller 
```
curateRawTweetsPaginated:function(req,res){ // this is for the business owner
	var classification;
	if(!req.params.classification)
		classification='curation_required';
	else 
		classification=req.params.classification;
	var page=req.query.page||1;
	var tweets_from=req.query.tweets_from;//we'll show tweets greater than this id
	var limit=req.query.limit||40;//we'll show these many tweets in a page
	var pg={
		u:req.user,
		pagination:{
			page:page
		}
	};
	var marked=0;

	var locals={
		pg:pg,
		title:'Curate raw tweets',
		description:'Mark the tweets that teach',
		item:'',
		classification:classification,
		filter:{}, // this is used by the front end filter
		tweets:[],
		tweets_from:tweets_from,
		track_id:req.query.track,
	}
	var filter={};
	sails.log.debug('\n\n\n\n\n --------_________----------');
	sails.log.debug('curateRawTweetsPaginated');
	// sails.log.info(locals);
	if(classification=='curation_required'||classification=='educational'||classification=='neutral'||classification=='spam'||classification=='curate_later')
	{
		async.auto({
			getListofLists:function(callback){
				var select =['name','description','type','id','createdAt','updatedAt'];
				List.find({type:'list'}).exec(callback);
			},
			getListOfTracks:function(callback){ // getting list of tracks
				var select =['name','description','type','id','createdAt','updatedAt'];
				List.find({type:'track'}).exec(callback);
			},
			getListofDomainExperts:function(callback){ // getting list of influencers
				var select = ['name','id','createdAt','updatedAt','twitter','image_url','username','description'];
				User.find({is_influencer:true}).exec(callback);
			}, 
			generateFilter:function(callback){ //setting filter - list/track or influencer
				var filter={};
				if(req.query.list || req.query.track){
					var list;
					if(req.query.list){
						locals.filter.type='list';	
						list=req.query.list;
					}
					else{
						locals.filter.type='track';
						list=req.query.track;
					}
					List.findOne({id:list}).populate('people').exec(function(err,list){
						filter.user=[];
						// sails.log.info(list);
						list.people.forEach(function(people){
							filter.user.push(people.id);
						});
						locals.filter.text=list.name;
						callback(err,filter);
					})

				}else if(req.query.influencer){ // this is to filter content from one influencer

					User.findOne({username:req.query.influencer}).exec(function(err,influ){
						// sails.log.info(influ);
						if(!err)
							filter.user=influ.id;
						locals.filter.type='influencer';
						locals.filter.text=influ.name;
						callback(err,filter);
					});
				}
				else
					callback(null,filter);
			},
			getCountOfCurationRequired:['generateFilter',function(results,callback){ // getting count of curation_required
				var filter=results.generateFilter;
				filter.classification='curation_required';
				Raw_tweet.count(filter).exec(callback);
			}],
			getCountOfEducational:['generateFilter',function(results,callback){ // getting count of educational
				var filter=results.generateFilter;
				filter.classification='educational';
				Raw_tweet.count(filter).exec(callback);
			}],
			getCountOfNeutral:['generateFilter',function(results,callback){ // getting count of neutral
				var filter=results.generateFilter;
				filter.classification='neutral';
				Raw_tweet.count(filter).exec(callback);
			}],
			getCountOfSpam:['generateFilter',function(results,callback){ // getting count of spam
				var filter=results.generateFilter;
				filter.classification='spam';
				Raw_tweet.count(filter).exec(callback);
			}],
			getCountOfCurateLater:['generateFilter',function(results,callback){ // getting count of curate_later
				var filter=results.generateFilter;
				filter.classification='curate_later';
				Raw_tweet.count(filter).exec(callback);
			}],
		},function(err,results){
			if(err)
				throw err;
			locals.lists=results.getListofLists;
			locals.tracks=results.getListOfTracks;
			locals.influencers=results.getListofDomainExperts;
			locals.count={
				curation_required:results.getCountOfCurationRequired,
				educational:results.getCountOfEducational,
				neutral:results.getCountOfNeutral,
				spam:results.getCountOfSpam,
				curate_later:results.getCountOfCurateLater,
			};
			console.log('all done');
			var filter=results.generateFilter;
			filter.classification=classification;
			locals.last_tweet=0;
			if(tweets_from>=1)
				filter.id={'<':tweets_from};
			Raw_tweet.find(filter).sort('id DESC').limit(limit).exec(function(err,tweets){
				locals.pg.pagination.total_pages=locals.count[classification]/limit;//total # of pages
				if(err)
					throw err;
				if(tweets.length>0)
					locals.last_tweet=tweets[tweets.length-1].id;
				locals.tweets=tweets;
				GeneralService.sendJsonOrHtmlRes(req,res,'curator/curate_raw_tweets',locals);
			});
		});
	}
	else
		res.send('Unknown status');
},
```




## Screenshot
![[Pasted image 20210312082505.png]]
