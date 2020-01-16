# any_conatiner
a simple json like container, implemented as std::variant.

```c++
using any_int_type = std::int64_t;
using any_key_type = std::variant<std::string, any_int_type>;
class any_value_type;
using any_vector = std::vector<any_value_type>;
using any_int_map = std::unordered_map<any_int_type, any_value_type>;
using any_str_map = std::unordered_map<std::string, any_value_type>;
class any_value_type: public std::variant<any_int_type, double, bool, std::string, any_vector, any_int_map, any_str_map>
```

## depends

cpp17

[nolhmann/json](https://github.com/nlohmann/json)


## content
`encode` convert any primitive type and std container to json
`decode` decode the json to specific primitive type or std container
`any_value` a json like container, but support int as key.


