@layer components {  
  @keyframes move {  
    from {  
      transform: translateY(100%);  
    }  
    to {  
      transform: translateY(-100%);  
    }  
  }  
  
  .animated-button {  
    --color: #fff;  
    --top: 0;  
    --side: 0;  
    --bottom: 0;  
  
    position: relative;  
  
    .top,  
    .bottom {  
      position: absolute;  
      overflow: hidden;  
      right: calc(var(--side) * -1);  
      left: calc(var(--side) * -1);  
      background-size: 100% 2px;  
      pointer-events: none;  
    }  
  
    .top {  
      top: calc(var(--top) * -1);  
      bottom: 50%;  
      background-image: linear-gradient(to top, transparent 50%, var(--color) 50%);  
      background-position: left bottom;  
      mask-image: radial-gradient(50% 90% at 50% 100%, black, transparent);  
  
      &::before {  
        content: '';  
        position: absolute;  
        top: calc(100% - 4px);  
        left: 0;  
        width: 100%;  
        transform: translateX(100%);  
        height: calc(100% - var(--top) + var(--bottom));  
        background-image: linear-gradient(to bottom, var(--color) 0, transparent 4px);  
        background-position: left top;  
        animation: move 5s linear infinite;  
      }  
    }  
  
    .bottom {  
      top: 50%;  
      bottom: calc(var(--bottom) * -1);  
      background-image: linear-gradient(to bottom, var(--color) 50%, transparent 50%);  
      background-position: left top;  
      mask-image: radial-gradient(50% 90% at 50% 0%, black, transparent);  
  
      &::before {  
        content: '';  
        position: absolute;  
        transform: translateX(100%);  
        top: 0;  
        left: 0;  
        width: 100%;  
        height: 100%;  
        background-image: linear-gradient(to bottom, var(--color) 0, transparent 4px);  
        background-position: left top;  
        animation: move 5s linear infinite;  
      }  
    }  
  }  
}