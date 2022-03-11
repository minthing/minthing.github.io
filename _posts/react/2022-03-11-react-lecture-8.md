---
title: "리엑트 공부 : 8th week"
categories:
  - react
tags:
- react
---

### context api
데이터가 전역적으로 사용되어야할 때 유용 

```javascript
import react, { useReducer, createContext, useMemo } from 'react';


export const TableContext = createContext({
  tableData: [],
  dispatch: () => {},
});

...

const MineSearch = () => {
    const [state, dispatch] = useReducer(reducer, initialState);

    const value = useMemo(() => ({tableData: state.tableData, dispatch}), [state.tableData]);

    return (
        <TableContext.Provider value={value}>
            <Form />
            <div>{state.timer}</div>
            <Table />
            <div>{state.result}</div>
        </TableContext.Provider>
    );
}
```