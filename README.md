
<!-- # ![mg-builder](/img~/mg-builder.png) -->

# Lesson 2

Developing Mobile Game lesson for Ankara university - Week 2

At the beginning of the lesson , "Package Manager" will be mentioned.
Then we will import Dotween and CarttonFX unitypackages from asset store.

## Demo 1 

* Scene Works
* Motion
* FixedUpdate

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo1.png"></td>

  </tr>
 </table>

 ```csharp

using UnityEngine;

public class Player : MonoBehaviour
{
    private const float velocity = 700f;

    private void FixedUpdate()
    {
        transform.position += new Vector3(0f, 0, 0.001f) * velocity;
    }
}

  ```

  ## Demo 2

* PlayerPrefs
* PlayerPrefs editor

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo2.png"></td>

  </tr>
 </table>

   ```csharp

public class Demo2 : MonoBehaviour
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
            PlayerPrefs.SetInt("Score", 9);
            PlayerPrefs.SetFloat("percentage", 0.67f);
        }
    }

}

  ```

## Demo 3

* DontDestroyOnLoad

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo3.png"></td>

  <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo3_2.png">
    </td>

  </tr>
 </table>

 ```csharp

public class Demo3_First : MonoBehaviour
{

    private Button btn_GoToScene2;

    private void Awake()
    {
        btn_GoToScene2 = GameObject.Find("Btn_GoToScene2").GetComponent<Button>();

        btn_GoToScene2.onClick.AddListener(delegate
        {
            SceneManager.LoadScene("Demo3_Second");
        });

    }
}

public class Demo3_Second : MonoBehaviour
{
    private Button btn_GoToScene1;

    private void Awake()
    {
        btn_GoToScene1 = GameObject.Find("Btn_GoToScene1").GetComponent<Button>();
        btn_GoToScene1.onClick.AddListener(GoToScene1);
    }

    private void GoToScene1()
    {
        SceneManager.LoadScene("Demo3_First");
    }
}


public class Demo3Manager : MonoBehaviour
{

    #region Singleton

    public static Demo3Manager Instance { get; private set; }

    private void Singleton()
    {
        if (Instance != null && Instance != this)
        {
            Destroy(this);
        }
        else
        {
            Instance = this;
            DontDestroyOnLoad(gameObject);
        }
    }
    #endregion

    private void Awake()
    {
        Debug.Log("Awake");

        Singleton();
    }

    private void Start()
    {
        StartCoroutine(DebugLogIEnumerator());
    }

    IEnumerator DebugLogIEnumerator()
    {
        var yieldReturn = new WaitForSeconds(0.3f);

        while (true)
        {
            yield return yieldReturn;
            Debug.Log("Demo3Manager");
        }
    }

}

  ```

  ## Demo 4

* Animator
* Animation Clip - Loop Time
* Animation Event
* Animation Speed

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo4.png"></td>

  </tr>
 </table>

 ```csharp

public class Demo4 : MonoBehaviour
{
    public void Trigger_AnimationEvent()
    {
        Debug.Log("I am at the ground...");
    }
}

  ```


