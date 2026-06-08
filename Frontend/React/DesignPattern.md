# Design Patterns

1. Render-Prop Design pattern

    - prop is a function with return value to be rendered inside the component
    - it allow sharing logic
    ```js
        <Pagination data={data} renderRow={function(item){  
            return <div className="text-white/80"> {item} --- hellp from app </div>
        }} /> 

    // component
    function Pagination({ data, renderRow }) {
        return (
            <div>
                {data.map(item => renderRow(item))}
            </div>
        );
    }
    ```
