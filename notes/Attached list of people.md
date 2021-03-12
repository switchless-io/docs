# Attached list of people

![[Pasted image 20210312073350.png]]

```
<div class="ui ten wide column">
    <div class="ui user_cards">
        <div class="ui segments">
            

            
            <h4 class="ui secondary top attached header">People in this list - <%=track.people.length%></h4>
            <% _.each(track.people,function(user){ %>
                <div class="ui attached segment">
                    <div class="ui comments">

                        <div class="comment">
                            <a class="avatar" href="/u/<%=user.username%>">
                            <img src="<%=user.image_url%>">
                            </a>
                            <div class="content">
                                <a class="author" href="/u/<%=user.username%>"><%= user.name%></a>
                                <div class="metadata">
                                    <span class="date"><%= user.username%></span>
                                    <a href="/curator/user/<%=user.id%>/edit">edit</a>
                                </div>
                                <div class="text">
                                    <span style="color: #888888">
                                        <%if(user.details&&user.details.reviews_count){%>
                                            <%=user.details.reviews_count%> recommendations
                                        <%}%>
                                        <br>
                                        <span class="ui <%- user.collect_tweets==false?'red':'green'%> label">collect_tweets</span>
                                        <span class="ui <%- user.twitter_profile?'green':'red'%> label">twitter_profile.id - <%- user.twitter_profile?user.twitter_profile.id:''%></span>
                                        <br>
                                        <br>
                                        
                                    </span>
                                    <button class='ui tiny button remove_user_from_list' data-user-id='<%=user.id%>'>remove</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            <% }) %>
            <div class="ui add_pple_list segment">
                <div class="ui form">
                    <div class="field">
                        <label>Add User</label>
                        <div class="ui search" id="search_user">
                            <div class="ui icon input">
                                <input class="prompt" id="user_name" type="text" name="user_name" placeholder="Select user">
                                <i class="search icon"></i>
                            </div>
                            <div class="results"></div>
                        </div>
                    </div>
                    <div class="field" style="display: none">
                        <label>User ID</label>
                        <input type="text" id="user_id" name="user_id" placeholder=" User ID" >
                    </div>
                    <button class="ui button add_user" type="submit">Add</button>
                </div>
            </div>
        </div>
    </div>
</div>
```

![[Pasted image 20210312073537.png]]
This also contains an attached form. 

## Javascript needed for form
```
<script type="text/javascript">
    $(document).ready(function(){


        $('button.add_user').click(function(){
            // window.location = $(this).attr('data-link');
            // console.log($('#user_id').val());
            var data={user_id:$('#user_id').val(),add_to:<%=track.id%>};
            // console.log(data);
            //update backend
            $(this).addClass('loading');
            $.post("/api/c/add_to_list",data, function(responseText, status,result){
                    // alert("Data: " + data + "\nResult: " + result);
                    console.log("result");
                    console.log(result);
                    console.log(data);
                    location.reload();
                   
            });
        });
        $('button.remove_user_from_list').click(function(){
            var data={user_id:$(this).attr('data-user-id'),list_id:<%=track.id%>};
            $(this).addClass('loading');
            $.post("/api/c/remove_from_list",data, function(responseText, status,result){
                    // alert("Data: " + data + "\nResult: " + result);
                    console.log("result");
                    console.log(result);
                    console.log(data);
                    location.reload();
            });
        })

        $('.ui.checkbox').checkbox();
        $('#search_user').search({
            apiSettings: {
              url: '/search/user/?q={query}'
            },
            fields: {
              results : 'users',
              title   : 'username',
              description : 'name',
              url     : false,
            },
            minCharacters : 3,
            onSelect:function(result,response){
                $('#user_id').val(result.id);
                return true;
            }
        });
    });
</script>
```