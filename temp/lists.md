```scss
// #region Lists ====================== // 

// List-Styles ================== //
// initial, none, inherit

// Unordered ==================== //
// disc, circle, square

// Ordered ====================== //
// decimal
// upper-alpha, lower-alpha,
// upper-greek, lower-greek,
// upper-latin, lower-latin,
// upper-roman, lower-roman


dl dl,
dl ol,
dl ul,
ol dl,
ol ol,
ol ul,
ul dl,
ul ol,
ul ul {
  margin: 0;
  padding: 0;
}

ul, ol {
      margin-bottom: 2rem;

  li {
    margin-left: 1rem;

    ol, ul {
      padding-top: 0rem;
      margin-bottom: 1rem;
    }
  }
}

ol {  
    list-style: decimal;
  ol {
    list-style: lower-alpha;
    ol {
      list-style: lower-roman;
    }
  }
}

// ul {  
//     list-style: disc;
//   ul {
//     list-style: circle;
//     ul {
//       list-style: square;
//     }
//   }
// }


// Definition lists.
dl {
    margin-bottom: 1rem;

  dt {
    font-size: var(--h8);
    font-weight: bolder;
  }

  dd {
    // margin-left: 1rem;
  }

  dd + dt {
    padding-top: 1rem;
  }
}
// #endregion Lists ====================== // 
```
