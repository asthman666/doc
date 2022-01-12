    import React, {Component} from 'react';

    export default class DynamicContainer extends Component{
        render() {
            // set the props.content to content
            // set the props.placeholder to placehoder, the placehoder has the default value '...'
            // set the props.hideWhenEmpty to false, the hideWhenEmpty has the default value false
            // set props other fields and values to rest, rest maybe include html props
            const {content, placeholder='...', hideWhenEmpty = false, ...rest} = this.props;
            if(content){
                rest.dangerouslySetInnerHTML={__html: content};
            }

            if(!content && hideWhenEmpty){
                return null; // don't render this component
            }

            return (
                <div {...rest}>
                    {!content?placeholder:null}
                </div>
            );
        }
    }
