---
title: React系列之分享一个自适应高的iframe组件
date: 2017-07-17T19:33:33.000Z
tags: React
---
在网页里面先要嵌入iframe,总是得要解决iframe高度的问题.

那我们在React下,该怎么做到呢?

```javascript
class FullheightIframe extends Component {
  constructor() {
    super();
    this.state = {
      iFrameHeight: "0px"
    };
  }

  render() {
    return (
      <iframe
        style={{
          width: "100%",
          height: this.state.iFrameHeight,
          overflow: "visible"
        }}
        onLoad={() => {
          const obj = ReactDOM.findDOMNode(this);
          this.setState({
            iFrameHeight: obj.contentWindow.document.body.scrollHeight + "px"
          });
        }}
        ref="iframe"
        src={this.props.src}
        width="100%"
        height={this.state.iFrameHeight}
        scrolling="no"
        frameBorder="0"
      />
    );
  }
}
```