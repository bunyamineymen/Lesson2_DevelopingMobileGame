
<!-- # ![mg-builder](/img~/mg-builder.png) -->

# Lesson 2

Developing Mobile Game lesson for Ankara university - Week 1

## Demo 1 

* PlayerPrefs
* PlayerPrefs editor

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo1.png"></td>

  </tr>
 </table>

   ```csharp

public class Demo1 : MonoBehaviour
{

    private TextMeshProUGUI txt_Variable;

    private void Awake()
    {
        txt_Variable = GameObject.Find("Txt_Variable").GetComponent<TextMeshProUGUI>();

        if (PlayerPrefs.HasKey("Variable"))
        {
            txt_Variable.text = PlayerPrefs.GetString("Variable");
        }
    }

    private void Start()
    {
        if (!PlayerPrefs.HasKey("Variable"))
        {
            PlayerPrefs.SetString("Variable", "This is variable !!!");
        }
    }

}

  ```


