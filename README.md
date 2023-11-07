using UnityEngine;
using System.Collections;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public Transform gunTransform;
    public GameObject bulletPrefab;

    private void Update()
    {
        float horizontalInput = Input.GetAxis("Horizontal");
        float verticalInput = Input.GetAxis("Vertical");
        Vector3 moveDirection = new Vector3(horizontalInput, 0, verticalInput).normalized;

        // Move the player
        transform.Translate(moveDirection * moveSpeed * Time.deltaTime);

        if (Input.GetButtonDown("Fire1"))
        {
            Shoot();
        }
    }

    void Shoot()
    {
        // Create and fire a bullet
        GameObject bullet = Instantiate(bulletPrefab, gunTransform.position, gunTransform.rotation);
        Rigidbody bulletRigidbody = bullet.GetComponent<Rigidbody>();
        bulletRigidbody.AddForce(gunTransform.forward * 10f, ForceMode.Impulse);
    }
}
