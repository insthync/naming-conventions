# Unity Project

### Coding
[ตามนี้เลย](https://unity.com/how-to/naming-and-code-style-tips-c-scripting-unity)

- พวกชื่อ Namespace, Class, Struct, Public Field, Property, Function เป็นแบบ `PascalCase` หมด
- พวก Private/Protected Field ให้มี Prefix เป็น `_` ตามด้วยชื่อเป็นแบบ `camelCase`
- พวกชื่อตัว
เช่น

```
namespace Company.GameName.Gameplay
{
    public class Character
    {
        public int MaxHp = 100;
        private int _currentHp;
        public string CurrentHp
        {
            get => _currentHp;
            set {
                if (_currentHp == value)
                    return;
                _currentHp = value;
                NotifyHpChanged();
            }
        }

        public bool IsDead => _currentHp <= 0;

        private void NotifyHpChanged()
        {
        }

        public void Revive()
        {
            if (IsDead)
                return;
            CurrentHp = MaxHp;
        }
    }
}
```
  

### Asset
[]
