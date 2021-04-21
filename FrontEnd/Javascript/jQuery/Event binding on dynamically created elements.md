### For example, if your page was dynamically creating elements with the class name `dosomething` you would bind the event to a parent which already exists (this is the nub of the problem here, you need something that exists to bind to, don't bind to the dynamic content), this can be (and the easiest option) is `document`.

    $(document).on('mouseover mouseout', '.dosomething', function(){
        // what you want to happen when mouseover and mouseout 
        // occurs on elements that match '.dosomething'
    });

## Any parent that exists at the time the event is bound is fine. 
### For example

    $('.buttons').on('click', 'button', function(){
        // do something here
    });

would apply to

    <div class="buttons">
        <!-- <button>s that are generated dynamically and added here -->
    </div>


# Result:

    $('#registered_participants').on(
        'click', 
        '.new_participant_part',          
        function() {

        }
    )

> [event-binding-on-dynamically-created-elements](https://stackoverflow.com/questions/203198/event-binding-on-dynamically-created-elements)

> [event-delegation](https://learn.jquery.com/events/event-delegation/)