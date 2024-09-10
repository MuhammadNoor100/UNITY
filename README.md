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
