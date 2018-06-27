# Ansible filter: get_attr

This filter overcomes Ansible's lack of variable substitution within dict keys.

* Issue: https://github.com/ansible/ansible/issues/17324


## Usage

```yaml
# Just to set some variables
- set_fact:
    key1: "Name"
    val1: "my-name"
    key2: "tier"
    val2: "dev"

# Here we actually use variables
- set_fact:
    key_val:
      - key: "{{ key1 }}"
        val: "{{ val1 }}"
      - key: "{{ key2 }}"
        val: "{{ val2 }}"

# The filter will actually reorder the above array into a dictionary.
- debug:
    msg: "{{ key_val | get_attr('key', 'val') }}"
```

This will result in the following output:
```json
{
  "key_val": {
    "Name": "my-name",
    "tier": "dev"
  }
}
```

## Integration

Copy `get_attr.py` into your roles `filter_plugins/` directory.
