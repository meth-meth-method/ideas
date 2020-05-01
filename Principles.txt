* ## Never overwrite data when reading inputs

    ```
    const source1 = {
      a: 123,
      b: 456,
    };

    const source2 = {
      a: 987,
      c: 654, 
    };

    function createBadConsumer() {
      const data = {};
      return {
        consume(source) {
          Object.assign(data, source);
        },
        show(key) {
          return data[key];
        }
      }
    }

    function createGoodConsumer() {
      const sources = [];
      return {
        consume(source) {
          sources.push(source);
        },
        show(key) {
          for (const source of sources) {
            if (source[key]) {
              return source[key];
            }
          }
        }
      }
    }
    ```

    Diagnosing why `show()` is giving the wrong data is much more likely to obscure the error.
