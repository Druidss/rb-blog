---
id: reactProblem
title: reactProblem
author: Adrian Yang
author_title: Front End Engineer
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [react, JavaScript, FroneEnd]
---

# 1 react中父组件调用子组件的方法

引用场景在进行上传这个业务的过程中， 将upload组件 作为上传组件的子组件。这个时候与服务器交互，父组件（上传组件）需要拿到upload组件中的上传的图片在服务器的图片名称。

这个场景下父组件需要直接调用子组件的方法（来获取到服务器response中的图片名称）

父组件

```jsx
class AddUpdate extends Component {
  constructor() {
    super();
    this.picRef = React.createRef();
    this.richText = React.createRef();
  }
    
onFinish = async(values) => {
    let detail = this.richText.current.getRichText()
    console.log(detail)
}
    
   <Form.Item 
      label="商品详情"
      wrapperCol={{md:16}}
   >
      <RichTextEditor ref={this.richText} />
   </Form.Item>
}
```



子组件方法

```jsx
 getRichText = () => {
    const {editorState} = this.state
    return draftToHtml(convertToRaw(editorState.getCurrentContent()))
  }
```

> 1. 子组件需要获取父组件的信息，这通过`props`就可以解决；
> 2. 父组件需要知道子组件的信息，这可以通过`ref`解决。