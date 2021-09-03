# All about select element in jQuery

## How to get the selected element?

`Element.find("option:selected")`

## How to get the element's selected value?

`Element.val()`

## How to get the element's selected text?

`Element.find("option:selected").text()`

## How to empty the element?

`Element.empty()`

## How to add option to select element?

    var options = Element.children();
    Element.append(options);

    Element.append(
        $('<option>', 
            {
                value: 1,
                text: 'My option'
            }
        )
    );


> [adding-options-to-a-select-using-jquery](https://stackoverflow.com/questions/740195/adding-options-to-a-select-using-jquery?page=1&tab=votes#tab-top)