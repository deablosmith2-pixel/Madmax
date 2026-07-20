using 
BlackEngine;

public class PlayerController : MonoBehaviour
{
    public float forwardSpeed = 10f;
        public float laneDistance = 3f;            public float doublejump Force = 7f;
                public float laneChangeSpeed = 10f;

                    private CharacterController controller;
                        private Vector3 moveVector;
                            private int currentLane = 1;
                                private bool isSliding = false;

                                    void Start()
                                        {
                                                controller = GetComponent<CharacterController>();
                                                    }

                                                        void Update()
                                                            {
                                                                    moveVector.z = forwardSpeed;

                                                                            // Gravity
                                                                                    if (controller.isGrounded)
                                                                                            {
                                                                                                        if (Input.GetKeyDown(KeyCode.Space))
                                                                                                                    {
                                                                                                                                    moveVector.y = jumpForce;
                                                                                                                                                }
                                                                                                                                                        }
                                                                                                                                                                moveVector.y += Physics.gravity.y * Time.deltaTime;

                                                                                                                                                                        // Lane switching
                                                                                                                                                                                if (Input.GetKeyDown(KeyCode.LeftArrow))
                                                                                                                                                                                        {
                                                                                                                                                                                                    currentLane = Mathf.Max(0, currentLane - 1);
                                                                                                                                                                                                            }

                                                                                                                                                                                                                    if (Input.GetKeyDown(KeyCode.RightArrow))
                                                                                                                                                                                                                            {
                                                                                                                                                                                                                                        currentLane = Mathf.Min(2, currentLane + 1);
                                                                                                                                                                                                                                                }

                                                                                                                                                                                                                                                        float targetX = (currentLane - 1) * laneDistance;
                                                                                                                                                                                                                                                                Vector3 targetPosition = transform.position;
                                                                                                                                                                                                                                                                        targetPosition.x = Mathf.Lerp(transform.position.x, targetX, Time.deltaTime * laneChangeSpeed);
                                                                                                                                                                                                                                                                                transform.position = targetPosition;

                                                                                                                                                                                                                                                                                        // Slide
                                                                                                                                                                                                                                                                                                if (Input.GetKeyDown(KeyCode.DownArrow))
                                                                                                                                                                                                                                                                                                        {
                                                                                                                                                                                                                                                                                                                    isSliding = true;
                                                                                                                                                                                                                                                                                                                                Invoke("StopSliding", 1f);
                                                                                                                                                                                                                                                                                                                                        }

                                                                                                                                                                                                                                                                                                                                                controller.Move(moveVector * Time.deltaTime);
                                                                                                                                                                                                                                                                                                                                                    }

                                                                                                                                                                                                                                                                                                                                                        void StopSliding()
                                                                                                                                                                                                                                                                                                                                                            {
                                                                                                                                                                                                                                                                                                                                                                    isSliding = false;
                                                                                                                                                                                                                                                                                                                                                                        }
                                                                                                                                                                                                                                                                                                                                                                        }