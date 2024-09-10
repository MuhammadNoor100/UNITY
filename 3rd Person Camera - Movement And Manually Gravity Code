using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraPos : MonoBehaviour
{
    [SerializeField] Transform player;
    [SerializeField] Vector3 getOff;
    private float XRotation;    
    private float YRotation;
    [SerializeField] float Sensitivity = 1;



    private void LateUpdate()
    {

        XRotation += Input.GetAxis("Camera Y") * Sensitivity;
        XRotation = Mathf.Clamp(XRotation, -20, 40);
  
   
        
        YRotation += Input.GetAxis("Camera X") * Sensitivity;
        
        
        var playerRotation = Quaternion.Euler(XRotation, YRotation, 0);      
        transform.position = player.position + playerRotation * getOff;
        transform.rotation = playerRotation;
    }

    public Quaternion PlayerR => Quaternion.Euler(0,YRotation, 0);



}





It's also attached with the camera code. 3rd person movement and also manually gravity




public class PlayerMovement : MonoBehaviour
{
    [SerializeField] float inputHorizontal;
    [SerializeField] float inputVertical;
    public CameraPos PlayerRotation;
    [SerializeField] float speed = 3.0f;
    CharacterController characterController;
    [SerializeField] float Groundradius = 0.2f;
    [SerializeField] Vector3 groundGetOff;
    [SerializeField] LayerMask GroundLayer;
    [SerializeField] float YSpeed;
    Quaternion rotationOfQuaternion;
    Animator animator;
    bool IsGround;





    private void Start()
    {
        
        PlayerRotation = Camera.main.GetComponent<CameraPos>();
        animator = GetComponent<Animator>();
        characterController = GetComponent<CharacterController>();
    }




    private void Update()
    {
        inputHorizontal = Input.GetAxis("Horizontal");
        inputVertical = Input.GetAxis("Vertical");
        float AbsoluteValue = Mathf.Abs(inputHorizontal) + Mathf.Abs(inputVertical);

        var playerMovement = new Vector3(inputHorizontal,0, inputVertical);
        var playerRot = PlayerRotation.PlayerR * playerMovement;


 
        if (IsGround== true)
        {
            YSpeed = -0.8f;
        }
        else
        {
            YSpeed += Physics.gravity.y * Time.deltaTime;
        }


        

        var velocity = playerRot * speed;
        velocity.y = YSpeed;

        characterController.Move(velocity * Time.deltaTime);

        if (AbsoluteValue > 0)
        {
          
            rotationOfQuaternion= Quaternion.LookRotation(playerRot);
        }
        transform.rotation = Quaternion.RotateTowards(transform.rotation, rotationOfQuaternion, 500f * Time.deltaTime);
        animator.SetFloat("AbsoluteValue", AbsoluteValue);
    }


    void GroundCheck()
    {
     IsGround = Physics.CheckSphere(transform.TransformPoint(groundGetOff), Groundradius, GroundLayer);

    }


    private void OnDrawGizmos()
    {
        Gizmos.color = Color.yellow;
        Gizmos.DrawSphere(transform.TransformPoint(groundGetOff), Groundradius);
    }

}

